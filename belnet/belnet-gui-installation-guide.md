---
description: BelNet GUI Installation Guide for Windows & Linux
---

# BelNet GUI Installation Guide

## **Windows**

**Download BelNet GUI for windows from the .exe file below:**

{% code fullWidth="true" %}
```
https://deb.beldex.io/Beldex-projects/belnet-gui/belnet-gui-2.0.0-win64.exe
```
{% endcode %}

## **Linux**

**Download BelNet GUI for Linux using the guide below:**

### Step 1: Add the key

Enter the following command to add the keys

```sh
sudo curl -L https://deb.beldex.io/pub.gpg | sudo apt-key add - && echo "deb https://deb.beldex.io/apt-repo stable main" | sudo tee /etc/apt/sources.list.d/beldex.list
```

### Step 2: Update the certificate

Enter the following command into the terminal to install and update the certificate

```sh
sudo apt install ca-certificates && sudo apt update
```

### Step 3: Install BelNet GUI

Enter the following command to complete the BelNet GUI installation

```sh
sudo apt install belnet-gui
```
