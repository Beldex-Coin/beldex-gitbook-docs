# Master Node Express Setup

Thinking of running a Beldex Master Node? Great! The guide below will help you configure a device with the necessary Master Node software packages, and stake $BDX to register the node on the Beldex network.

> Note: This guide assumes some familiarity with the command line and running a Linux server. For a more detailed walkthrough, check out our full Master Node setup guide.

### Operating system requirements

One of:

* Ubuntu 20.04 ("focal")
* Ubuntu 22.04.05 ("Jammy Jellyfish")
* Ubuntu 25.04.5 ("Noble Numbet")

> Note: There are strict uptime requirements for Master Nodes. It is **strongly discouraged** to run a Master Node on a device that will not be continuously on-line. We recommend running your Master Node on a VPS with a reputable provider.

### Firewall Configuration

If you are using a firewall then you should ensure that the following ports are open and reachable:

* Port 29089 (storage server to storage server)
* Port 29090 (client to storage server)
* Port 19090 (blockchain syncing)
* Port 19095 (Master Node to Master Node)
* Port 1090 (UDP, not TCP, unlike all of the above; Belnet router data)

### Super Fast guide - New Master Node Setup

Configuring a new Beldex Master Node is pretty simple and straight forward. For running a Master Node you need to get your VPS's public IP address. The Master Node requies a public IP address. You cna get the public IP address of your VPS using the below command.

```
curl -s ifconfig.me
```

Copy your public IP address, you may require to add the IP address manually if the deb setup will not fetch your IP address automatically.

Run the below 5 commands on your Linux server (these commands will work on Debian and Ubuntu; modifications may be necessary for other Linux distributions):

```
curl -L https://deb.beldex.io/pub.gpg | sudo apt-key add -

echo "deb  https://deb.beldex.io/apt-repo stable main" | sudo tee /etc/apt/sources.list.d/beldex.list

sudo apt install ca-certificates

sudo apt update

sudo apt install beldex-master-node

```

The services will run via systemd as `beldex-node.service`, `beldex-storage-server.service and beldet-router.service`&#x20;

Once the blockchain has synced to the server (which can take several hours, If sync from the beginning), your Master Node will be ready to be staked. You can use the `beldexd status` command to check the sync progress.

### Express guide - New Master Node Setup

#### Step 1: Initial repository set-up

To add the Beldex repository, run the following commands.

> Note: You only need to follow this step once, to set up the repository. The repository will subsequently be automatically updated whenever you fetch new system updates.

This first command installs the public key used to sign the Beldex Master Node packages:

```
sudo curl -L https://deb.beldex.io/pub.gpg | sudo apt-key add -
```

The second command tells `apt` where to find the packages.

```
echo "deb https://deb.beldex.io/apt-repo stable main" | sudo tee /etc/apt/sources.list.d/beldex.list
```

Then resync your package repositories with:

```
sudo apt update
```

#### Step 2: Beldex Master Node configuration

To configure your Master Node, simply install the `beldex-master-node` package:

```
sudo apt install beldex-master-node
```

This will detect your public IP (or allow you to enter it yourself) and automatically update the `/etc/beldex/beldex.conf` configuration file with the necessary additional settings to run a Master Node.

#### Step 2: Belnet Status Check

Check whether your Belnet router setup is done correctly or not using the below command.

```
systemctl status belnet-router.service
```

If the Belnet router is setup correctly you will get the message shown in the below screenshot.

<figure><img src="../../.gitbook/assets/Belnet-router-active-status.png" alt=""><figcaption></figcaption></figure>

If the Belnet router is not setup correctly you will get the error message as shown in the image below&#x20;

<figure><img src="../../.gitbook/assets/Belnet-router-failed-status.png" alt=""><figcaption></figcaption></figure>

The issue is because the public IP and  port of your VPS is not set in `belnet.ini` file, so you need to set it manually, the file is located in the path `/var/lib/belnet/router/belnet.ini` .  Add the IP address and port in the file as follows

```
public-ip=<Your Public IP Address>

public-port=1090
```



Congratulations! Your Master Node is now ready to be registered and staked.

### Staking your Master Node

#### Preparing your Master Node for registration

To prepare your master Node for registration, run the following command:

```
beldexd prepare_registration
```

This will prompt you for some registration details, then output a registration command. Copy the output from this command in preparation for the next step.

> Note: You can safely run this command multiple times if you change your mind about some of the registration questions before you submit the registration.

#### Staking and registering your Master Node

To stake and register your Master Node, open the Beldex Electron wallet. Make sure your wallet has a balance of at least 10,000 $BDX to meet the Master Node staking requirement (less if you're configuring a shared Master Node). Navigate to the `Master Nodes`tab > `Registration` section, and paste the output from the above command, then click **Register Master Node**.

Done! Your staking transaction will now be submitted to the network. After a short delay, your Master Node will be registered and start contributing to the network (and receiving rewards!).

#### Checking registration status

You can easily check if your Master Node is registered on the network. First, connect to the VPS where the Master Node is running and run the following command to retrieve your Master Node's public key:

```
beldexd status
```

This will output a bunch of information about your Master Node, but there's one part we're interested in at this stage: The long string of random letters and numbers after the characters `MN:` . This string is your Master Node's public key, used to identify your Master Node on the list of registered and operational Master Nodes. Select and copy the public key (do not copy any of the surrounding information).

You can now jump onto [explorer.beldex.io](https://explorer.beldex.io), open the full list of active Master Nodes, and use `Cmd+F`/`Ctrl+F` to check if your Master Node's public key appears in the list.

#### Upgrading  - For Existing Master Node

When a new release is available, upgrading is as simple as syncing your repositories:

```
curl -L https://deb.beldex.io/pub.gpg | sudo apt-key add -

sudo apt update
```

Then installing any updates using:

```
sudo apt upgrade
```

> Note that this will install both updated Beldex packages _and_ any available system updates (this is generally a good thing!)

During the upgrade, the running instance of `beldexd` will be restarted to ensure that the updated `beldexd` is now active.

If, for some reason, you want to install _only_ updated Beldex package upgrades, but not other system packages, then instead of `sudo apt upgrade` you can use:

```
sudo apt upgrade beldexd 
```

```
sudo apt upgrade beldex-storage-server 
```

```
sudo apt upgrade belnet-router 
```

### Back-ups

Backing up your Master Node's secret key. Will allow you to easily recover or migrate your Master Node

Reveal MN secret key:

```
beldex-mn-keys show /var/lib/beldex/key_ed25519
```

Restore from MN secret key:

```
beldex-mn-keys restore /var/lib/beldex/key_ed25519
```

Having trouble? Just [head to our Support section](https://discord.com/invite/Hj4MAmA5gs).
