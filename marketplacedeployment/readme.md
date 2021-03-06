# Deploy Azure IoT Edge Enabled Linux VM

## Azure Market Place Offering

Use a preconfigured virtual machine to get started quickly, and easily automate and scale your IoT Edge testing.

This **Ubuntu Server 16.04 LTS** based virtual machine will install the latest Azure IoT Edge runtime and its dependencies on startup, and makes it easy to connect to your IoT Hub.


## Steps to Create VM

1. Click <a href="https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft_iot_edge.iot_edge_vm_ubuntu?tab=Overview" target="_blank">here</a> to deploy an Azure IoT Edge enabled Linux VM.

    ![Azure IoT Edge VM](images/01_marketplace_offering.png)

2. Click **Get It Now** button and click **Continue** on the browser. Please note: You might need to sign in.
    ![Azure IoT Edge VM](images/02_get_it_now_continue.png)

3. Logs you into Azure portal. Click **Create** button
    ![Azure IoT Edge VM](images/03_create_vm.png)

4. Provide Subscription details and resource group. Give your VM an unique name. Also, select password radio button and provide user and password to use later
    ![Azure IoT Edge VM](images/04_create_vm_details.png)

   Allow SSH ports by selecting the inbound ports radio button
    ![Azure IoT Edge VM](images/05_allow_ssh_port.png)

5. Validation process happens and a web page is presented. Click **Create** button.

6. Deployment completes in around 3 minutes.
    ![Azure IoT Edge VM](images/06_deployment_complete.png)

7. Click on **Go To Resource** button

8. Click on **Connect** button and copy the ssh command. This allows us to connect to our VM. 

    ![Azure IoT Edge VM](images/07_connect_ssh.png)

9. Click on **Cloud Shell icon** (Located on the top right section of the portal), opens a cloud shell browser. Copy the ssh command and press enter or you can use **shell.azure.com** in your browser

    ![Azure IoT Edge VM](images/08_cloud_shell_ssh.png)

    You will be prompted with **Bash** or **PowerShell**. Select **Bash** for this workshop

    ![Shell](images/18_shell_bash.png)

    Select your subscription and create storage account

    ![Shell](images/19_storage_mount.png)

    You will get a prompt 

    ![Shell](images/20_shell_created.png)


In the Azure Cloud Shell add your SSH login infomation you just copied. Right click and select paste to paste ssh login command. 

    ```Linux
    ssh iotedgeadmin@<Your VM IP>
    ```
    
    
    
    Provide your VM pasword you gave when you created the VM and press **Enter**

10. Confirm Azure Edge Runtime is installed on the VM by entering the following command:

    ```Linux
    iotedge version
    ```

    ![Azure IoT Edge VM](images/09_edge_version.png)

### Add Edge Device to IoT Hub

Use VSCode to create Edge Device.


#### Add Edge Device

Select Create Edge Device option


    ```editor
    Press Control + Shift + P in the VSCode editor

    Search for:

    > Azure IoT Edge Create IoT Edge
    ```

![Add Device](images/10_create_edge_device.png)

Enter Device ID and press **Enter**

![Device Id](images/11_create_edge_device.png)

#### Edge Device Created

Edge device created, you can check the response in VSCode output

![Device Created](images/12_created_edge_device.png)

### Get IoT Hub Connection String

Use IoT Toolkit to copy IoT Hub connection string.

```editor
Press Control + Shift + P in the VSCode editor

Enter >Azure IoT Hub

```

Select **Copy IoT Hub Device Connection String** option

![Connection String](images/13_device_connection_string.png)

You will be presented with device list. Select your edge device

![Connection String](images/14_select_edge_device.png)

When you press **Control+V** you will see a string like below

```editor
HostName=rvedgehub.azure-devices.net;DeviceId=mylinuxedge;SharedAccessKey=sZTt4dg3lB/i39b5L6vWuNuZxH7CCWzz7T6q8eA19PQ=
```

Another way to get connection string is to go to Portal and find your IoT Hub -> -> IoT Edge Device -> Your Edge Device ->  Connection string - primary key. Copy the connection string primary key.

![Connection String](images/15_device_details.png)

### Connect Edge Device to IoT Hub

Go To cloud shell. **ssh** into your Linux VM.
**sudo** into your VM as root

```Linux
sudo su -
```

and run the following command. Replace your IoT Hub connection string.

```editor
/etc/iotedge/configedge.sh  "<your_iothub_edge_device_connection_string>"
```

![Set Connection String](images/16_attach_device.png)

EdgeAgent System Module is sent to the edge device

![Module List](images/17_edge_module_list.png)

 Continue on to the next part of the lab: [Module 4: Add an Edge Module and Deploy to Edge Device](https://hellotechie.github.io/azureiotedgelab/edgemodule/)
