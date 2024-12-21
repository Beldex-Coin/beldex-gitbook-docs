# Master Node Registration Guide



**Server Requirements**

* **Operating System**: Ubuntu 18.04 or higher
* **Storage**: Minimum 40GB
* **RAM**: 2-4 GB
* **CPU**: 1 Core

***

#### **Step 1: Initial Master Node Setup**

1.  **Add the Public Key**: Install the public key required to verify and sign the Beldex Master Node packages:

    ```bash
    sudo curl -L https://deb.beldex.io/pub.gpg | sudo apt-key add -
    ```
2.  **Add the Package Repository**: Inform the package manager about the location of the Beldex repository:

    ```bash
    echo "deb https://deb.beldex.io/apt-repo stable main" | sudo tee /etc/apt/sources.list.d/beldex.list
    ```
3.  **Update Package Repositories**: Resynchronize your package manager to include the new repository:

    ```bash
    sudo apt update
    ```
4.  **Install the Master Node Package**: Set up your Master Node by installing the required package:

    ```bash
    sudo apt install beldex-master-node
    ```

    * This command will detect your public IP or prompt you to enter it manually and update the configuration file (`/etc/beldex/beldex.conf`) with the necessary settings.

***

#### **Step 2: Verify Services Status**

**Beldex Node:**

Check if the `beldex-node` service is running correctly:

```bash
systemctl status beldex-node.service
```

**Command Output:**

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXc6j3Oe8LKibMgGuBypwsMhzZTWm9cQKLAWvyuNRmp1XkqHzoa3XBAOoa01u1SDF70c9tioNztJvCV0oi67J_YnQQknfiB-ZaDJkhoo281MvbAInjCnhj7Q8Dq0aXrbm657RnvzIw?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

**Beldex Storage Server:**

Verify the status of the `beldex-storage-server` service:

```bash
systemctl status beldex-storage-server.service
```

**Command Output:**

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcC9HHlx20jbqq1wVvrCeNtm26oJjisYF1lwpm8O5vZwRnRktCYGDH3jjR-fRDlhr_IHeAQT6tsFZmi8zJnYl_f_tdj8zNRIAEXVr1GI3vhy_IA3q6UyNMOH-8D63DTZ_jYownLWA?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

_**Note:** Ping to daemon will start after 57000 blocks_

**Belnet Router:**

Confirm the `belnet-router` service is operational:

```bash
systemctl status belnet-router.service
```

**Command Output:**

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdjQvtEQMBgG1aPY4OYry33d3GuPqSInkcnyPcbMCTLp-ZtFvvTUXFoLY1F2ZLUmlHCFU7X8cJOI3FPlipaYVQiTwmPikp8cj2V7RGwJl-hmxcq99nq--SAPID00btK-RCekAWDQw?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

***

#### **Step 3: Check Status of the Daemon**

**Beldex Daemon:**

*   Verify the status of `beldexd`:

    ```bash
    beldexd status
    ```

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZNLi_YK45Ol4A1c8lavE7b8EkUdYvsTssjUqqqI02709bxXzSciqH-xkHhh6noxXzS4TXNgK4PTge8GlkdDl-ptIa9uvMUxdlb1qEchVS_YZP1WKfcg4ZkaIDvlBWlJrO_trUAA?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

* If the Master Node public key and last pings are not displayed, restart the `beldex-node` service:

```bash
systemctl restart beldex-node.service
```

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXc1wVRC9nUgluBPcFOkyjTJQvvdGhoQw8GVj1tAQFILEvfunm01VzZf3Hxdj_E3uK6bORWhWf7EHS3Q_VSZimdsdI2Dl42vZlaC55HhY0eYM-PFmmwFFJjJl8_txSur1kKXF9M9Ow?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

Status after received ping from the storage server and belnet

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZNLi_YK45Ol4A1c8lavE7b8EkUdYvsTssjUqqqI02709bxXzSciqH-xkHhh6noxXzS4TXNgK4PTge8GlkdDl-ptIa9uvMUxdlb1qEchVS_YZP1WKfcg4ZkaIDvlBWlJrO_trUAA?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

_**Note:** Ping from storage server and belnet is mandatiry for master node registration_

***



#### **Step 4: Register Master Node**

1.  Once the node synchronization reaches 100%, prepare the Master Node registration:

    ```bash
    beldexd prepare_registration
    ```

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmD265xhhXaxCCqO6zYHkOSP7Ag6jeyvpROPR3BNW6_e0semTsQfgXGBynngHHaRLnmT-dzaUALMSSx1iazpiZrZ3RirteyKvGIbDhulpNEd119F25dI90TpkDMFgD7s8pGXYeJg?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

Enter the wallet address when prompted, and follow the instructions carefully.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcCdz6MbzVpMJ94emtxtfeQvdRmZa9tTOq-L2grOkIJdWOyk01XDF8OUg6OhHYajv4nJjswYTOG7KGMeIg6rOkJlpOwRMqQ8g3dXPniKvaYtiG2YvwBVqJ1XCW3m2QpMOtYti_cMA?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

After providing all the required prompt data, the `register_master_node` string will be generated.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfwYrzCAhyQwaea1IzXjyhiSbabmj7hf_4P6DJxrNPV4byoYOYCWKhbRGcJST8nuiaKGnDhXuYUrdMi2txO-EfR4tvYzNiBFPvAKIhLRru2jJWQTX_aiiCrRkyAFUJyh5LUWbN0gw?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

Open the Electron Desktop wallet and  enter the generated `register_master_node` string in the registration section as shown in the below screenshot

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXccQBX2GwFpK79Sb1uVdWBd3VEzkIEbrLnjnpQzW24iYj4Q2PJu9x6x50onN4XvUKTyWO88LrYp8BapRtbzMI69fF_f9K6KdPeqHogVEa1XYpHKs1_d3X9uGepOVPgqOgg6Cdge?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

When you click the "Register Master Node" button, the Master Node will be successfully registered, and a confirmation message stating "Master Node registered successfully" will be displayed.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfu2A7sDIXqBjnO4-XRFz4vJAhHuPzdjbdSoPacRscdxpnvIAGlM5G3Op2vg6A2z_Jt3k76Fp4LNBiz4R6-6tQHFm4jOxIMHLIuYXLLIik73yChHaUY8o19ZTV-h91QjCaANnlBMg?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

Congratulations !!! You are now successfully registerd the master node and the reward will be credited directly to the wallet which you used to regiuster the master node

***

#### **Error Handling and Troubleshooting**

**1. Storage Server Not Pinging:**

If the `beldex-storage-server` does not respond to pings in the `beldexd` status, restart the service:

```bash
systemctl restart beldex-storage-server.service
```

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcf7LeQF-WijGlb_kiewPKmGJ2SiGXelnnrIB_mvSJRRzEVNxaQIpwzAcKhmEQ8iRtZzVEq4khVAWtbSCNXbHLiX0OAXs5NVBuvVhbXnI31VlgJUVi2BjNjzg_F2rFDjN1niAH8sw?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

**2. Belnet Router Not Pinging:**

If the `belnet-router` ping is not received:

```bash
systemctl restart belnet-router.service
```

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeUzh62moK0Ki-FLq7Q3EbKDDlnagWVJRdJasYTyD7rF915AHKc74-XyjoUD9erMDnG0HUYSNX1R7MVM9vlsSjU5QNDQt-yqolXa9NC28SmZ21g4PdqjC4SB4CapfSJemoW5sOr?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

**3. Belnet Router Bootstrap Error:**

If `belnet-router` fails to bootstrap, follow these commands:

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdrmnNLGQttXEpirKbaoZsDcdyEEiTx5kGsoCDAedg1ohQcKJk2I92ZUYtIliI48CP50Jvs_QiYqfkHTfaPjjYIfpp1KKNK7pXe9JKpfdR8EcZvUOOqgcNqAkKcEpp9MPi7_xKvFw?key=9jIxUVTok0XDRH__-NQrXLqR" alt=""><figcaption></figcaption></figure>

*   Check the service status:

    ```bash
    systemctl status belnet-router.service
    ```
*   Navigate to the Belnet directory:

    ```bash
    cd /var/lib/belnet
    ```
*   Bootstrap Belnet:

    ```bash
    belnet-bootstrap
    ```
*   Restart the `belnet-router` service:

    ```bash
    systemctl restart belnet-router.service
    ```
* This process ensures the `belnet-bootstrap` binary downloads the required files to `/var/lib/belnet` and initiates pings.
