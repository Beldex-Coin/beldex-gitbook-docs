---
description: A comprehensive guide to setting up your exit node
---

# Exit Node Setup Guide

## System Requirements <a href="#docs-internal-guid-bbd4629f-7fff-9315-5af1-8e508d2bf909" id="docs-internal-guid-bbd4629f-7fff-9315-5af1-8e508d2bf909"></a>

Below are the system requirements and the minimum specifications of dedicated server or VPS

| S. No. | Spec             | Note                     |
| ------ | ---------------- | ------------------------ |
| 1      | CPU Cores        | 2 or more                |
| 2      | RAM              | 4 GB                     |
| 3      | Storage          | 40 GB SSD                |
| 4      | Higher Bandwidth | At least 1 GB preferable |

### &#x20;**Step 1: Install BelNet on your VPS**

Copy and paste the following link into the terminal

This will download the Belnet binaries from cloud

```shell
wget https://github.com/Beldex-Coin/belnet/releases/download/v0.9.8/belnet-linux-x86_64-v0.9.8.zip
```

Unzip the file using the following command&#x20;

```shell
unzip belnet-linux-x86_64-v0.9.8.zip
```

**Execution**

* install vim editor using the following command

```shell
sudo apt install vim
```

* Install tmux in your system

```shell
sudo apt install tmux
```

* Create a tmux session&#x20;

```shell
tmux new -s belnet
```

* Run the Belnet binary

```shell
sudo ./belnet
```

* Download the bootstrap file using belnet-bootstrap

```shell
sudo ./belnet-bootstrap
```

### &#x20;**Step 2: Configure Belnet.ini using vim**

* Go to Belnet config directory

```shell
cd /var/lib/belnet/
```

* Edit the belnet.ini file by entering the following command&#x20;

```shell
vim belnet.ini
```

Add the following lines under the \[router] section or uncomment the following by removing the #.

This will configure the number of connections that an exit node can maintain.

```yaml
netid = belnet
worker-threads=0 (It uses all threads)
min-connections=18
max-connections=20
```

Add the following lines under the \[network] section or uncomment the following by removing the #.

```yaml
keyfile=/var/lib/belnet/exit.private
ifaddr=10.0.0.1/16
ifname=exit0
hops=2
paths=8
exit=true
```

<figure><img src="https://lh6.googleusercontent.com/6RlJnzDRHin-wb8S1ikVW6HeXv7AEl7t7eGCxha9UCnwn89NJiqzFnJJXsrV5NYcDlrQR7QlkcbJKXg5N5hgY0iysvivGPxTGAjuOh3v3Awz4b8hTnCC8gzvGaSSDOZUjz5uEaWqYlZJGHaTQUUIZ_vaQ63zOHZbHcaxrt7gUNMc7GiMaWKw4ok2CJOXaQ" alt=""><figcaption></figcaption></figure>

### &#x20;<a href="#docs-internal-guid-8cc649b8-7fff-54d8-5bf6-ab23f3276b57" id="docs-internal-guid-8cc649b8-7fff-54d8-5bf6-ab23f3276b57"></a>

### Step 3 Enable IP Forwarding via ''sysctl'' <a href="#docs-internal-guid-8cc649b8-7fff-54d8-5bf6-ab23f3276b57" id="docs-internal-guid-8cc649b8-7fff-54d8-5bf6-ab23f3276b57"></a>

Open the following folder&#x20;

```shell
sudo vim /etc/sysctl.conf
```

Add the following lines. This will allow IP forwarding for both IPV4 and IPV6&#x20;

```shell
net.ipv4.ip_forward=1
net.ipv6.conf.all.forwarding=1
```

<figure><img src="https://lh4.googleusercontent.com/pBRsiT7R3lUJbRjiyyQZQKGkVgvR0rk3YyBaordEHh3C3B90FlA-PpoRKjhtFYQhdqWNtd3UJ2WA9i43SBUO3mx6WGDwDyHTN6WedEjzVSyx8bd1leOjTH36NjnW0Uoh3hsCohigsGl2wY1dTl55yikAyCs41hnbHQUUD-ZHVCsJqwFEM-yjHI6-H-5GMg" alt=""><figcaption></figcaption></figure>

Press `ESC + :wq` to save and exit to `/etc/sysctl.conf`

Enable the changes using the following command

```shell
sysctl -p
```

<figure><img src="https://lh3.googleusercontent.com/BTOZdG3EoZgAbW09VbSLbbiBaT1A7jByhj1N0YEms7RGxMgvvKkFLRy6H06dftEtTTKwfPFOZzPSviwZaOyJiaAs6ewmC5cRKY4gs0cR-kBKxGlbkTDi0U3wYHdHJkML_m8SQ4_NYt2Lynt5r0eTd-i244iFKvbFsp7aIPb_eBjhSDW_aaKSD9yf_75TmA" alt=""><figcaption></figcaption></figure>

### &#x20;<a href="#docs-internal-guid-5a576d0a-7fff-b16f-18e2-48a9324d77b4" id="docs-internal-guid-5a576d0a-7fff-b16f-18e2-48a9324d77b4"></a>

### Step 4: Setup firewall <a href="#docs-internal-guid-5a576d0a-7fff-b16f-18e2-48a9324d77b4" id="docs-internal-guid-5a576d0a-7fff-b16f-18e2-48a9324d77b4"></a>

Please check firewall status using the following command

```shell
iptables -S
```

Default result should return the following

&#x20;_-P INPUT ACCEPT_

&#x20;_-P FORWARD ACCEPT_

&#x20;_-P OUTPUT ACCEPT_

<figure><img src="https://lh3.googleusercontent.com/HyDxIj_vqsPxWe6BYecUU5H_i8Xj-L3096q0XOxPb28zy9eI95fTd2cvbVR46eCQZPSEO91GmbyV2txeunnJXwdiJAUl0J7oN1VCfPqgX6ep5nVvazJiDZ-cPH3_Wn3VJm24yfoOKgr5RWb72gGHOg2ZGONa6TU0z2ya1fKr1M886ptca6b34LwcS8x-RQ" alt=""><figcaption></figcaption></figure>

**Add firewall rules for IPv4**

Copy and paste the following commands

```shell
iptables -t nat -A POSTROUTING -s 10.0.0.0/16 -o eth0 -j MASQUERADE

iptables-save

ip6tables -t nat -A POSTROUTING -s fd00::a00:0/112 -o eth0 -j MASQUERADE

ip6tables-save
```

<figure><img src="https://lh5.googleusercontent.com/Q2alDwTdej0YbSOQLNsaQ2gCcCHv7GRccaCNL8cas_8l9RIGDF_FSYBX_b6r7RK56jEokzNoc7GmLZQdDE5gIPHyh7odnk2R254djQP5kYFucuHkda-LDz7psCg4I3h4ydwG0IP1M09RLoW3uYXdZj82dlt70H9CopvHiQ8cTauwOgKSWDDZHcydVWgH-A" alt=""><figcaption></figcaption></figure>

**Add route for Belnet interface's IPv6**

```shell
ip -6 route add fd00::a00:0/112 dev exit0
```

It is beneficial to block ports for Simple Mail Transfer Protocol (SMTP), SMTP over Secure Sockets Layer (SSL), SMTP over Transport Layer Security (TLS), Internet Relay Chat (IRC) and IRC over SSL. This is non-mandatory but may protect your exit node from Distributed Denial Of Service (DDOS) attacks. For more details, kindly check with your VPS host.

```shell
for port in 25 465 587 666{0,1,2,3,4,5,6,7} 6697 ; 
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport $port -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport $port -j REJECT --reject-with tcp-reset
```

Now it is completed

Then, enter the following commands,

```shell
iptables-save

ip6tables-save
```

<figure><img src="https://lh6.googleusercontent.com/pq-MxqRpjvbGiMC0xaPQScBm43ppJ6BK5PLhw4FAckJY88G0JU6oOk4bX4DF8eZE_ZxfJ40iL1rqoUMDcXMmN8eAVLXH1gii5DrSR4SiXKlCmnpFYSPvKqIpFo7XHolnHrWGlT6Gejp2yCy_5zgGhORm6O6H1Je3ZSlQzqbv15C61l7RD-_EhjQ8mTyMqA" alt=""><figcaption></figcaption></figure>

The above commands unroll to:

```shell
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 25 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 465 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 587 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6660 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6661 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6662 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6663 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6664 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6665 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6666 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6667 -j REJECT --reject-with tcp-reset
iptables -A FORWARD -s 10.0.0.0/16 -p tcp -m tcp --dport 6697 -j REJECT --reject-with tcp-reset

iptables-save

ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 25 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 465 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 587 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6660 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6661 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6662 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6663 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6664 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6665 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6666 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6667 -j REJECT --reject-with tcp-reset
ip6tables -A FORWARD -s fd00::a00:0/112 -p tcp -m tcp --dport 6697 -j REJECT --reject-with tcp-reset

ip6tables-save
```

**Make firewall settings persistent after rebooting the system by using the command given below**&#x20;

```shell
apt install iptables-persistent
```

Select **Yes** on the pop-up window to save current rules to install both for IPv4 and IPv6.

<figure><img src="https://lh6.googleusercontent.com/9W_l-yycUKgwiVcRPOeIM94vfWslSQ4876Vyref_mMySf870yeWdQBsMW5OI65_upFXySmUg9a67pzVAgT3IxwVHXJcOATcxFRWLLIYvI5x-mhRmV76MKgviAIDv0Qhv-SaH70iPmMpbWQ6l7U329WZMTHFHJ1qwNppuEVmRdJ82vDX-w5hNs5gVMdtKrw" alt=""><figcaption></figcaption></figure>

Run Belnet&#x20;

```shell
sudo ./belnet
```

### Step 5: Fetch your permanent .bdx address  <a href="#docs-internal-guid-eb3a8252-7fff-74e5-6415-22f7fc422032" id="docs-internal-guid-eb3a8252-7fff-74e5-6415-22f7fc422032"></a>

Enter the following command to fetch your address

```shell
host -t cname localhost.bdx 127.3.2.1
```

<figure><img src="../.gitbook/assets/Exit Node Setup Screenshot 9.jpg" alt=""><figcaption></figcaption></figure>

To check if your exit node is publicly hosted, enter the following command&#x20;

```shell
nslookup .bdx address
```

### Step 6: If you face any errors, you can troubleshoot your DNS using the following command

Open the resolv.conf file&#x20;

```shell
sudo vim /etc/resolv.conf
```

Please add the following nameserver in the file

```
nameserver  127.3.2.1
```

Save and exit the file using the command `ESC + :wq`
