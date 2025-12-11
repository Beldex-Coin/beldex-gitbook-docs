---
description: A guide to setup master node using docker
---

# Master Node Docker Setup

The easiest and most efficient way to set up a master node is by using Docker. Follow these two simple steps to set up a master node with Docker. We have provided a shell script to handle all the heavy lifting for you.

> Note: This guide assumes some familiarity with the command line and running a Linux server. For a more detailed walkthrough, check out our full Master Node setup guide.

### Step 1 :  Create or Download the shell file

Copy the below code to a shell file `master-node-deploy.sh`&#x20;

```sh
#!/bin/bash
  
# Define the Docker image and container name
IMAGE_NAME="beldex/beldex-master-node:v1"
CONTAINER_NAME="beldex-mn-node"
SERVICE_NAME="beldex-testnet-storage-server.service"

# Run the Docker container
echo "Running the Docker container..."
docker run --network=host --privileged --name $CONTAINER_NAME -v /sys/fs/cgroup:/sys/fs/cgroup:ro -d $IMAGE_NAME

# Give Docker a moment to start the container
sleep 5

# Fetch the container ID for the given container name
CONTAINER_ID=$(docker ps -q --filter name=$CONTAINER_NAME)

# Check if any container ID is found
if [ -z "$CONTAINER_ID" ]; then
  echo "No running container found with name: $CONTAINER_NAME"
  exit 1
else
  echo "Container ID for container $CONTAINER_NAME: $CONTAINER_ID"
fi

# Define the script to update the belnet.ini file
UPDATE_SCRIPT=$(cat <<'EOF'
IP=$(curl -sS http://api.ipify.org || true)
echo "IP for belnet: $IP"

# Update the beldex.conf file
sed -i -e "s/^master-node-public-ip=.*/master-node-public-ip=$IP/" /etc/beldex/beldex.conf

PRIVATE_IP=$(ip route get 1.2.3.4 | awk '{print $7}')
echo "PRIVATE_IP for belnet: $PRIVATE_IP"

sed -i -e "s/^public-ip=.*/public-ip=$IP/" /var/lib/belnet/router/belnet.ini

sed -i -e "s/^[[:space:]]*inbound=.*/     inbound=$PRIVATE_IP/" /var/lib/belnet/router/belnet.ini
EOF
)

# Execute the update script inside the Docker container
echo "Updating the belnet.ini,beldex.conf file inside the Docker container..."
docker exec $CONTAINER_ID bash -c "$UPDATE_SCRIPT"

# Confirm the update
if [ $? -eq 0 ]; then
  echo "belnet.ini,beldex.conf file inside container $CONTAINER_NAME with ID $CONTAINER_ID has been updated successfully."
else
  echo "Failed to update belnet.ini,beldex.conf file inside container $CONTAINER_NAME with ID $CONTAINER_ID."
  exit 1
fi

# stop the service inside the Docker container
echo "Stop the service inside the Docker container..."
docker exec -it $CONTAINER_ID systemctl stop $SERVICE_NAME

# Confirm the service restart
if [ $? -eq 0 ]; then
  echo "Service $SERVICE_NAME inside container $CONTAINER_NAME with ID $CONTAINER_ID has been stoped successfully."
else
  echo "Failed to stop service $SERVICE_NAME inside container $CONTAINER_NAME with ID $CONTAINER_ID."
  exit 1
fi
```

OR

```
wget https://deb.beldex.io/beldex-projects/master-node-docker/master-node-deploy.sh
```

### Step 2:  Register Master Node

> Make sure the node is fully synced before run this command

#### Check the node status

```
docker exec -it <CONTAINER_ID> beldexd status
```

You should receive an output similar to the screenshot provided. Ensure that the height of your node matches the current network height, which can be verified at [Beldex Explorer](https://explorer.beldex.io). If the heights do not match, allow the node to fully sync, which may take 4-5 hours.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-05 at 4.58.45 PM.png" alt=""><figcaption><p>node status</p></figcaption></figure>

#### Prepare for Registration

Once the node is fully synced, run the below command to register the master node

```
docker exec -it <CONTAINER_ID> beldexd prepare_registration
```

After successfully running the command, you will receive an output similar to the screenshot below. To complete the registration, execute the master node command from the output in your wallet.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-05 at 4.58.55 PM.png" alt=""><figcaption><p>master node registration</p></figcaption></figure>



{% hint style="info" %}
You can run all beldexd commands using docker. Run <mark style="color:blue;">`docker exec -it <CONTAINER_ID> beldexd --help`</mark> to get the list of commands
{% endhint %}
