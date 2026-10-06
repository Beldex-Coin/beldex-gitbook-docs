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
set -euo pipefail

IMAGE_NAME="beldex/beldex-master-node:v2"
CONTAINER_NAME="beldex-mn-node"
SERVICE_NAME="beldex-testnet-storage-server.service"

echo "Starting container..."
# choose the run command you want — simple example (Option A assumes the image runs the node directly)
docker run --network=host --privileged --name "$CONTAINER_NAME" -d "$IMAGE_NAME" || true

# give the daemon a second to settle
sleep 3

# Get container id even if it's exited
CONTAINER_ID=$(docker ps -aq --filter "name=^/${CONTAINER_NAME}$")

if [ -z "$CONTAINER_ID" ]; then
  echo "No container was created with name: $CONTAINER_NAME"
  exit 1
fi

# If it's not running, print logs and exit (helpful for debugging)
STATUS=$(docker inspect -f '{{.State.Status}}' "$CONTAINER_ID")
if [ "$STATUS" != "running" ]; then
  echo "Container $CONTAINER_NAME (ID $CONTAINER_ID) is not running. Status: $STATUS"
  echo "== docker logs =="
  docker logs "$CONTAINER_ID" || true
  echo "== docker inspect =="
  docker inspect "$CONTAINER_ID"
  exit 1
fi

echo "Container is running: $CONTAINER_ID"

# Update script to run inside the container (unchanged)
UPDATE_SCRIPT=$(cat <<'EOF'
IP=$(curl -sS http://api.ipify.org || true)
echo "IP for belnet: $IP"

sed -i -e "s/^master-node-public-ip=.*/master-node-public-ip=$IP/" /etc/beldex/beldex.conf

PRIVATE_IP=$(ip route get 1.2.3.4 | awk '{print $7}')
echo "PRIVATE_IP for belnet: $PRIVATE_IP"

sed -i -e "s/^public-ip=.*/public-ip=$IP/" /var/lib/belnet/router/belnet.ini
sed -i -e "s/^[[:space:]]*inbound=.*/     inbound=$PRIVATE_IP/" /var/lib/belnet/router/belnet.ini
EOF
)

echo "Updating files inside container..."
docker exec "$CONTAINER_ID" bash -lc "$UPDATE_SCRIPT"

echo "Stopping "$SERVICE_NAME"  inside the container..."
docker exec -it "$CONTAINER_ID" systemctl stop "$SERVICE_NAME" || {
  echo "Failed to stop service. Check service name or systemd status inside the container."
  docker exec "$CONTAINER_ID" journalctl -xe --no-pager || true
  exit 1
}

echo "Done."
```

OR

```
wget https://deb.beldex.io/Beldex-projects/master-node-docker/master-node-deploy.sh
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
