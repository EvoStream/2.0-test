---
title: Connecting to EMS
keywords: amazon
sidebar: emscloud_sidebar
permalink: emscloud_amazon_connectEMS.html
folder: emscloud
toc: true
---



After creating the EMS instance, you will need to connect to your EMS to use it. Here are the steps on how you can connect to EMS using **SSH Terminal**, **Windows PuTTy**, **EMS Web UI** and **EMS HTTP Based API**.



## Connecting to EMS on Linux

### A.	SSH via Terminal

Connecting to your new instance via SSH is exactly the same as connecting to any Linux EC2 computer. You will access it using the “ubuntu” user and use the .pem key you chose during Instance setup.

1. Locate the .pem (key file) in the terminal

2. Send command: `ssh –i ./<evostream-keys.pem> ubuntu@<public_IP>`

   **Note:** Public IP can be found on the Amazon instances. See Determining Public IP.

   ```
   test@ubuntu:~/Desktop$ ssh -i ./evostream-keys.pem ubuntu@52.91.237.115
   The authenticity of host '52.91.237.115 (52.91.237.115)' can't be established.
   ECDSA key fingerprint is ae:02:ee:41:ff:38:96:ab:78:7b:3a:e6:09:ed:1f:4c.
   Are you sure you want to continue connecting (yes/no)? 
   ```

3. Input "**yes**", press **Enter**

   ```
   Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 3.13.0-46-generic x86_64)

   	Documentation:  https://help.ubuntu.com/
    System information as of Wed Jan 20 09:11:53 UTC 2016
    System load:  0.0               Processes:           106
    Usage of /:   13.9% of 7.74GB   Users logged in:     1
    Memory usage: 2%                IP address for eth0: 11.22.33.44.55
    Swap usage:   0%
    Graph this data and manage this system at:
      https://landscape.canonical.com/
    Get cloud support with Ubuntu Advantage Cloud Guest:
      http://www.ubuntu.com/business/services/cloud
   ```






### B.	Windows PuTTy

#### B.1.	Pre-requisites

- PuTTY Generator

- PuTTY Secure Shell Client

- Key file

  ​


#### B.2.	Key File Conversion

EvoStream Media Server configuration can be accomplished using SSH and a client. Public AMI instances use a public/private key pair to log in instead of a password. The public key half of this pair is embedded in your instance, allowing you to use the private key half to log in securely without a password.

On Windows® operating systems, you can open a secure session to your Amazon EC2 instance by using the PuTTY Secure Shell client, which you can download [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

The first thing you’ll need to do is <u>convert</u> the private key. The PuTTY Secure Shell client doesn't natively support the private key format generated by Amazon EC2. Fortunately, PuTTY has a tool called **PuTTYgen** that you can use to convert your private key to the required PuTTY Private Key File (\*.ppk) format. To convert the \[key-pairname\].pem file that you created to a \[key-pair-name\].ppk file, do the following:

1. Run **PuTTY Key Generator**

2. Click **Load** button

   ![](images/emscloud/image14.jpg)

   ​

3. Select and open the **.pem file** that you want to convert in the Load private key window.

   **Note:** You'll need to select the All Files option in the File filter drop-down list to see PEM files in the file list.

   ​

4. Click **OK** in the PuTTYgen Notice window

   ![](images/emscloud/image15.png)

   ​

5. Click **Save private key** and save the file with the name **\[key-pair-name\].ppk**.




#### B.3.	Connecting via SSH

1. Run **PuTTY**

2. Select **Session** under the category tree

   ![](images/emscloud/image16.png)

   ​

3. Specify the destination you want to connect to:

   ![](images/emscloud/image17.png)

   **Host Name** – the public IP address in Amazon EC2 instance running EvoStream Media Server

   **Port** – 22 (default)

   **Connection type** – SSH

   ​

4. Select **Auth** under **Connection > SSH** in category tree

5. Click the **Browse** button to find and open the **\[key-pair-name\].ppk** file

   ![](images/emscloud/image18.jpg)

   **Note:** If you will be opening this same session later, you can save it for future use

   ***To save the session information:***

   On the Basic options for your PuTTY Session page, enter a name for the session in Saved Sessions, and then click the **Save** button

   ![](images/emscloud/image19.jpg)

   1. Click the **Open** button to open the secure SSH session. The first time you connect to your instance, you'll get a PuTTY Security Alert that references the first use of **\[key-pair-name\].pem**

   2. Click **Yes** to accept the security key

      ![](images/emscloud/image20.png)

   3. Logged in as "**ubuntu**"

      ![](images/emscloud/loggedin.JPG)



If you previously saved the SSH session information for this Amazon EC2 instance, do the following:

1. Run **PuTTY**

2. Select **Session** in the category tree

3. Select the Saved Session and then click the **Load** button

   ![](images/emscloud/image21.jpg)

4. Click the **Open** button to open the secure SSH session.

**Note:** You should see the login as: prompt in the SSH client window. Enter "**ubuntu**" as the username 

![](images/emscloud/image22.png)

![](images/emscloud/loggedin.JPG)



### B.	EMS Web UI

While most work with the EMS happens at the command line or through the HTTP based API calls, the EMS does have a Web UI that can be used. To access the UI simply point your browser at the proper URL: `http://<DomainOrPublicIP>:8888/EMS_Web_UI/index.php`

**< DomainOrPublicIP >** will need to be replaced with the Public Domain or Public IP of your new EC2 Instance.

**Note:** EMS should be running to be able to access the EMS Web UI.



#### B.1.	Determining Public IP

1. Sign in to *https://console.aws.amazon.com*

2. Click on the **EC2** under compute

   ![](images/emscloud/image23.jpeg)

3. In the Navigation pane of the EC2 Management Console, under Instances, click **Instances**.

4. Select the running instance.

5. In the lower pane, click the **Description tab**. The Public DNS value is the public domain name of your running instance and the Instance ID is the instances instance ID.

   ![](images/emscloud/image13.jpeg)

   ​

#### B.2. Login for Web UI

The Web UI is protected by default when using the EMS on AWS.  When accessing the Web UI you will be prompted for a username and password.

![](images/emscloud/authentication.JPG)

- Username: evostream

- Password: "Amazon Instance ID" - this will need to be obtained via your Amazon account.

  **Getting the Amazon Instance ID**

  **From Amazon Console**

  1. Sign in to *https://console.aws.amazon.com*

  2. Click on the **EC2** under compute

     ![](images/emscloud/image23.jpeg)

  3. Click on **Running Instances** under Resources

     ![](images/emscloud/image24.jpeg)

     ​

  4. Click on the **Instance Name** provided for the EMS, and look for the **Instance ID** given.  This will be your password.

     ![](images/emscloud/image25.jpeg)






### C.	HTTP Based API

For integration with the EMS at the software level, using the HTTP Based API is often much more useful.  The full set of API's available to you are found here: [API Definition](api_overview.html).

For the EMS on AWS, the HTTP based API is exposed, but it requires authentication to be used.  We call this **Proxy Authentication**. Basic Authentication is used and so just a username and password are required:

- Username: evostream
- Password: "Amazon Instance ID" - this will need to be obtained via your Amazon account as explained above.

**Command will take this general format:**

```
http://Username:Password@IPAddress:Port/apiproxy/CommandName?params=<base64EncodedString>
```

Run the command in a browser.  Copy the command in a browser URL then press **Enter**.

**Sample Command:** 

```
http://evostream:i-013c03dc9bab9d69f@52.91.237.115:8888/apiproxy/version
```

**Note:** username is “**evostream**” and password is the “**instance ID**”

See EMS [HTTP JSON CLI](userguide_telnet.html#http-json-cli) for more details.





## Connecting to EMS on Windows


### A.	Remote Desktop Connection

1. Run the **Remote Desktop Application**

2. Enter the details of the virtual machine image, click **Connect**

   **Computer** - the IP address of the image

   **Username** -Administrator

   **Password**- *see below*

   ​

   2.1.	How to obtain the password?

   To get the password, right click on the instance under the Instances list. Click **Connect** and you will be prompted with this:

   ![](images/emscloud/password.jpg)

   ​

   2.2. Click on **Get Password**. Choose the **[key-pair-name].pem** then click **Decrypt Password**. 

   A **password** will be shown on the window.

   ![](images/emscloud/decrypt.JPG)

   ​

3. Enter the **password** for the user, click **OK**

4. The connection will be established. Run EMS by double clicking the desktop shortcut icon or running the `run_console_ems.bat`. You can now use the EMS capabilities!

**Note:** The EMS is installed in `C:\EvoStream`. 



### B.	EMS Web UI

While most work with the EMS happens at the command line or through the HTTP based API calls, the EMS does have a Web UI that can be used. To access the UI simply point your browser at the proper URL: `http://<DomainOrPublicIP>:8888/EMS_Web_UI/index.php`

**< DomainOrPublicIP >** will need to be replaced with the Public Domain or Public IP of your new EC2 Instance.

**Note:** EMS should be running to be able to access the EMS Web UI.



#### B.1.	Determining Public IP

1. Sign in to *https://console.aws.amazon.com*

2. Click on the **EC2** under compute

   ![](images/emscloud/image23.jpeg)

3. In the Navigation pane of the EC2 Management Console, under Instances, click **Instances**.

4. Select the running instance.

5. In the lower pane, click the **Description tab**. The Public DNS value is the public domain name of your running instance and the Instance ID is the instances instance ID.

   ![](images/emscloud/image13.jpeg)

   ​

#### B.2. Login for Web UI

The Web UI is protected by default when using the EMS on AWS.  When accessing the Web UI you will be prompted for a username and password.

![](images/emscloud/authentication.JPG)

- Username: evostream

- Password: "Amazon Instance ID" - this will need to be obtained via your Amazon account.

  **Getting the Amazon Instance ID**

  **From Amazon Console**

  1. Sign in to *https://console.aws.amazon.com*

  2. Click on the **EC2** under compute

     ![](images/emscloud/image23.jpeg)

  3. Click on **Running Instances** under Resources

     ![](images/emscloud/image24.jpeg)

     ​

  4. Click on the **Instance Name** provided for the EMS, and look for the **Instance ID** given.  This will be your password.

     ![](images/emscloud/image25.jpeg)



### C.	HTTP Based API

The above instructions gave you access to the EMS via the command line.  For integration with the EMS at the software level, using the HTTP Based API is often much more useful.  The full set of API's available to you are found here: [API Definition](api_overview.html).

For the EMS on AWS, the HTTP based API is exposed, but it requires authentication to be used.  We call this **Proxy Authentication**. Basic Authentication is used and so just a username and password are required:

- Username: evostream
- Password: "Amazon Instance ID" - this will need to be obtained via your Amazon account as explained above.

**Command will take this general format:**

```
http://Username:Password@IPAddress:Port/apiproxy/CommandName?params=<base64EncodedString>
```

Run the command in a browser.  Copy the command in a browser URL then press **Enter**.

**Sample Command:** 

```
http://evostream:i-013c03dc9bab9d69f@52.91.237.115:8888/apiproxy/version
```

**Note:** username is “**evostream**” and password is the “**instance ID**”

See EMS [HTTP JSON CLI](userguide_telnet.html#http-json-cli) for more details.

