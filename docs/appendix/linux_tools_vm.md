---
title: Linux Tools VM
---

## Overview

We will deploy a Linux (CentOS) VM to use it as our workstation. 

## Deploying Linux Tools VM

1. In **Prism Central** > select **Menu** > **Compute and Storage > VMs**, and click **Create VM**

1.  Fill out the following fields:
    -   **Name** - *Initials*-Linux-ToolsVM
    -   **Description** - (Optional) Description for your VM.
    -   **Number of VMs** - 1
    -   **CPU(s)** - 4
    -   **Number of Cores per CPU** - 1
    -   **Memory** - 4 GiB
2.  Click **Next**
3.  Under **Disks** select **Attach Disk**
    -   **Type** - DISK
    -   **Operation** - Clone from Image
    -   **Image** - Linux_ToolsVM.qcow2
    -   **Capacity** - leave at default size
    -   **Bus Type** - leave at default SCSI Setting
4.  Click **Save**
5.  Under **Networks** select **Attach to Subnet**
    -   **VLAN Name** - Primary
    -   **Network Connection State** - Connected
    -   **Assignment Type** - Assign with DHCP
6.  Click **Save**
7.  Click **Next** at the bottom
8.  In **Management** section
    -   **Categories** - leave blank
    -   **Timezone** - leave at default UTC
    -   **Guest Customization** - 
        - **Script Type** - Cloud-init (Linux)
        - **Configuration Method** - Custom Script 
  
        <details>

          <summary>Do you need to create a SSH key pair?</summary>
           
           You can use any online ssh key generator if you are using Windows. Execute the following commands in you are in a Linux / Mac environment to generate a private key.
    
           ```bash
           ssh-keygen -t rsa -b 2048 -C "Created for Linux Tools VM"
           
           # follow prompts 
           # do not specify passphrase
           # once completed run the following command
           
           cat id_rsa.pub
           
           # copy the contents of the id_rsa.pub file to your cloudinit yaml file
           ```
        </details>

        - Paste the following script in the script window 
        
          ```yaml
          #cloud-config
          
          # Set the hostname
          hostname: myhost
          
          # Create a new user
          users:
            - default
            - name: nutanix
              groups: wheel, users
              ssh_authorized_keys:
              # Paste the generated public key here
              - ssh-rsa AAAAB3NzaC1....
              # You can also use the salter 1N or 6N format using OPENSSL (openssl passwd -1 -salt SaltSalt "yourplaintextpassword")
              # Paste the generated password here
              passwd: $1$SaltSalt$aOsqVFP2QULyFo5JYkOYB/
              shell: /bin/bash
              lock-passwd: false
              ssh_pwauth: True                 
          
          # Enable password authentication for root
          ssh_pwauth: True
          
          # Run additional commands
          runcmd:
          - 'sleep 10' # sleeping for the network to be UP
          - 'echo "nutanix ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers'
          
          # Run package upgrade
          package_upgrade: true
          
          # Install the following packages - add extra that you would need
          packages:
          - git
          - bind-utils
          - nmap
          - curl
          - wget 
          - vim
          - python3
          - python3-pip
          ```

9. Click on **Next**
10. Click **Create VM** at the bottom
11. Go back to **Prism Central** > **Menu** > **Compute and Storage** > **VMs**
12. Select your *Initials*-Linux-ToolsVM
13. Under **Actions** drop-down menu, choose **Power On**

    !!!note
            It may take up to 10 minutes for the VM to be ready.

            You can watch the console of the VM from Prism Central to make sure all the clouinit script has finished running.

14. Login to the VM via SSH or Console session, using the following command:

    ```bash
    ssh -i <your_private_key> -l nutanix <IP of LinuxToolsVM>
    ```
    ```bash title="Example command"
    ssh -i id_rsa -l nutanix 10.54.63.95
    ```

