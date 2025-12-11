---
description: A comprehensive guide to hosting your first MNApp
---

# MNApp Hosting Guide Using Nginx

The server specifications such as storage and bandwidth for hosting an MNApp are dependent on the user's requirements. For example, a video streaming platform may require more storage than an information sharing platform.&#x20;

However, you need a Linux system with Ubuntu 18.04 or 20.04 to run an MNApp.



## Step 1: Install BelNet on Your System and Generate Your Belnet Address

Download and run the binaries

Enter the following command into the terminal to download the Belnet binaries from cloud&#x20;

```shell
wget https://github.com/Beldex-Coin/belnet/releases/download/v0.9.8/belnet-linux-x86_64-v0.9.8.zip
```



Unzip the file using the following command&#x20;

```shell
unzip belnet-linux-x86_64-v0.9.8.zip
```

Run the Belnet binary

```shell
sudo ./belnet
```

Then, copy and paste the following command to open the belnet.ini file.

```shell
sudo vim /var/lib/belnet/belnet.ini
```

Scroll down to the \[network] section and configure the keyfile by giving it a name of your choice. Your MNApp private key will be stored in the following path. Here, we’ve named our keyfile, mnappkey.private

```
keyfile=/var/lib/belnet/mnappkey.private
```

Enter the following command and restart the Belnet client

```shell
sudo ./belnet
```

## Step 2: Find Your MNApp’s BelNet Address

To find your MNApp address, enter the following command.

```shell
host -t cname localhost.bdx 127.3.2.1
```

For example, this is the MNApp address for the Beldex explorer hosted on BelNet _**cw41adqqhykuxw51xmagkkb3fixyieat1josbux13jn6o973tqgy.bdx**_



## Step 3: Download and Install Nginx

Nginx is a dependency. So download and install it using the following commands

```shell
sudo apt update
sudo apt install nginx
```

Use the following command to check whether nginx is working

```shell
systemctl status nginx
```

## Step 4: Setup Your MNApp Web Page

Your web content goes into this directory&#x20;

Create a directory using the following command. Give a name to your directory. You can do this by replacing your\_own-directory in the command below with your directory name.&#x20;

```shell
sudo  mkdir /var/www/your_own_directory/
```

Place your html web page into this directory



## Step 5: Configure Nginx

Below is a sample configuration of Nginx&#x20;

Enter the following commands

```shell
sudo cd /etc/nginx/sites-available
sudo vim default
```

Now enter your directory’s name (established in Step 4) in place of your\_own\_directory in the command below.&#x20;

```shell
root /var/www/your_own_directory; 
```

Add the index file of your webpage here using the following command.&#x20;

Note: Replace your\_webpage with the filename that you want to assign to your index html file.

`index your_webpage.html;`&#x20;



Now choose a server name by entering the following command. Replace the sample BelNet address below with your MNApp’s BelNet address generated in Step 2.

```shell
server_name cw41adqqhykuxw51xmagkkb3fixyieat1josbux13jn6o973tqgy.bdx;
```

Save it by pressing `Esc` and then `:wq`

Restart Nginx using the following command&#x20;

```shell
sudo systemctl restart nginx.service
```

To access your MNApps, connect to BelNet and enter the MNApp’s BelNet address into a browser’s address bar

e.g. [http://cw41adqqhykuxw51xmagkkb3fixyieat1josbux13jn6o973tqgy.bdx/](http://cw41adqqhykuxw51xmagkkb3fixyieat1josbux13jn6o973tqgy.bdx/)&#x20;

Note: You cannot host a masternode and an MNApp in the same server. You cannot host a BelNet exit node and an MNApp in the same server.
