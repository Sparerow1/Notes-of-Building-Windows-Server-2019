# Installing and Configuring Hyper-V server

In this step I will be installing and configuring a Hyper-V server and install a VM within that Hyper-V server

The IP address is 192.168.1.116 and the name will be WIN2K19-HPV01

## *Basic set up for the new VM*

Setting up the basic configuration and virtualization engine new virtual machine

And add new Hyper-V role to WIN2K19-HPV01

1. Set up a VM and do the usual network set ups and domain joins
2.	Assigned it an IP address of 192.168.1.116 and name of WIN2K19-HPV01
3.	Check Virtualize Intel VT-x/EPT or AMD-V/RVI in the Processors section of the Virtual machine settings of the VM WIN2K19-HPV01
4.	Allocate 8GB of RAM to the VM
    - ![Virtualization settings](img/VM_virtualization_setting.png "Configure VM settings and virtulization engine")
5. Set up an OU in the main domain controller active directory
    - Under the PalmBeach OU of the YCFOREST.LOCAL active directory domain, locate the Users OU that we created earlier, and in it, create an IT OU and then create an administrator user called HyperVAdmin and put it in side the IT OU as well as assign it to the domain admin group(the user group that has all the domain admins in it, which will grant the HyperVAdmin account admin permissions in the domain)
    - We will be using HyperVAdmin as the account we use the set up the HyperV server
6. Add another 60GB drive to the HPV server and make a simple volume out of it
    - This one will be an E drive with the name HyperV
    - ![Configured new E drive](img/new_drive.png "Configured new E drive")
    - Put a copy of Windows server 2016 and 2019 ISOs in the drive
7. Add roles and features    
    - It will be a roles based feature
8. Select the HyperV role
    - If we did not select the Virtualize Intel VT-x/EPT or AMD-V/RVI in the Processors option in the VMware settings, we will definitely not get pass this part as the VM will be incompatible with the role
    - ![Add new Hyper-V role to the VM](img/add_role.png "Add new Hyper-V role to the VM")
9.	Leave the rest as default for now, we will further configure the settings later
10.	Let it install and restart


## *Configure Hyper-V settings*

Configure Hyper-V settings via Hyper-V manager

Configure basic network and hardware resources for Hyper-V VMs that will be installed in this server

1. Open up HyperV manager by going to the HyperV option at the left panel of the Server Manager after signing in and finishing up the installation
    - Right click on the server WIN2K19-HyperV01 and select HyperV Manager
    - ![Open up Hyper-V manager](img/hyper-v.png "Open up Hyper-V manager")
2. In the Hyper-V manager, find the WIN2K19-HPV01 server, right click on it, and select Virtual Switch manager
    - ![Open up Virtual Switch Manager](img/hyper-v14.png "Open up Virtual Switch Manager")
    - ![Open up Virtual Switch Manager](img/hyper-v2.png "Open up Virtual Switch Manager")
3. We will create all three types of virtual switches, External switch, internal switch, and private switch
    - External switch is what we need to get out to the internet with our VM
    - Internal switch is what we used to connect the HyperV virtual machines that we have in our WIN2K19-HPV01 server to each other and the host server(WIN2K19-HPV01)
        - We are installing Hyper-V VMs in the HPV01 server, which means from the perspective of those VMs in the server, HPV01 is the physical machine
        - This cannot allow those VMs to access the internet
    - Private switch can only allow Hyper-V VMs in the same host to talk to each other, it does not allow guest to host interaction
        - It does not allow internet access
4. Creating external switch
    - This is the switch that we will use, the other 2 we are doing it just for fun
    - Select the External option and then select Create Virtual Switch
    - Name: Ext-HPVSwitch
    - Allow management to the OS
    - ![Configure external switch](img/hyper-v3.png "Configure external switch")
    - Click apply and ok
5. Creating Internal switch
    - Select the internal option and click on Create Virtual Switch
    - Name: Int-HPVSwitch
    - ![Configure internal switch](img/hyper-v4.png "Configure internal switch")
        - Click on apply and ok to create the internal switch
6.	Create Private Switch
    - Select the private option and click on create virtual switch
    - Name: Pri-HPVSwitch
    - Click on Apply and ok
    - ![Configure private switch](img/hyper-v5.png "Configure private switch")
        - Click on appy and ok to create the private switch
7. Configuring Virtual Hard Disk
    - Select the server(HPV01) and go to HyperV settings by right clicking on it and selecting Hyper-V Settings
    - Click on the Virtual Hard Disks section on the left panel, and then browse to the directory that you have created for the storage of the virtual hard disk
        - I made a directory(HVData) in the E drive that I made earlier, and within it, I have another directory(Virtual_Hard_Disk) that holds my virtual hard disk
        - ![Configure virtual hard disk for Hyper-V VM](img/hyper-v6.png "Configure virtual hard disk for Hyper-V VM")
            - Configure virtual hard disk for Hyper-V VM
8.	Configure the path of the VMs(Where the Hyper-V VMs will be stored in the WIN2K19-HPV01 VM)
    - Go to the Hyper-V settings
    - I will be putting the VM at the HVData directory of the E drive of the server
    - ![Configure location of the VM](img/hyper-v7.png "Configure the location where the Hyper-V VMs will reside in WIN2K19-HPV01")
        - Configure the location where the Hyper-V VMs will reside in WIN2K19-HPV01


## *Create new Hyper-V VM and install Windows Server 2016 on it*

The settings for the Hyper-V VMs are now set up, we can now create a new Hyper-V VM and install Windows Server 2016 on it using the Windows Server 2016 ISO that we transferred over to WIN2K19-HPV01

1. Create a new Hyper-V VM on WIN2K19-HPV01
2. Right click on the HPV01 server in the left panel of the Hyper-V manager
3. Select New --> Virtual Machine
4. Name of the machine will be WIN2K16
    - This will be a 2016 server
    - ![Creating new Hyper-V virtual machine](img/hyper-v8.png "Creating new Hyper-V virtual machine on the environment of WIN2K19-HPV01")
5. This will be a generation 2 VM
    - ![Creating new Hyper-V virtual machine](img/hyper-v9.png "This will be a generation 2 VM")
6. Assign 2048MB of memory to this new VM
    - 2GB of memory = 2048MB
    -  ![Assign 2GB of memory](img/hyper-v10.png "Assign 2GB of memory to this VM")
        - 2GB of memory is assigned to this VM
7. Connection will be the external switch(Ext-HPVSwitch) that we created earlier
    - We want our Hyper-V VM to get internet access
    - ![Network switch is Ext-HPVSwitch](img/hyper-v11.png "Network switch is Ext-HPVSwitch")
8. 50GB of hard drive, with dynamic expansion and the Hard Disk path should be the same as the one we made earlier
    - ![Configured hard drive for this Hyper-V VM](img/hyper-v12.png "Configured hard drive for this Hyper-V VM")
    - I understand that my drive on WIN2K19-HPV01 does not have 50GB to allocate to the Hyper-V VM since it is only 60GB, but because this is an dynmanically expanding virutal hard disk, so it will actually take up less space once we create it
        - Dynamically expanding hard drive expand the virtual hard drive space with demand. Which means the hard drive starts out small, and the more you put into the hard drive the larger it gets, until it reaches a limt that we set, or the physical limit of the hard drive
            - In this case, the limit that we set is 50GB, meaning that our virtual hard drive will theorically expand to maximum of 50GB before stopping
            - But the virtual hard drive is small(like around 10 GB) when the machine is created
9. Select the Windows Server 2016 ISO and put it in the ISO path field
    - ![Configured installation file](img/hyper-v13.png "Configured installation file to the VM")
    - This will allow us to boot to the ISO file like booting to the Windows Server 2016 installation DVD to install the Windows Server 2016 onto the new Hyper-V VM
10. Read the summary of the VM settings, and then let it do its thing after clicking finish
11. After the VM has been created, it is now time to install Windows Server 2016 on the new Hyper-V VM
    - ![Booting to the Windows 2016 ISO](img/VM.png "Booting to the Windows Server 2016 ISO that we added to the Hyper-V VM to install Windows server 2016")
    - Booting to the Windows Server 2016 ISO that we added to the Hyper-V VM to install Windows server 2016
12. This one will be a 2016 Standard Desktop Edition
    - Standard Desktop Edition is lighter than the Datacenter one, and I do not have that much space nor RAM, so this is what I am going with
    - ![Select Standard Desktop Experience](img/VM2.png "Select Standard Desktop Experience")
13. Just let it do its thing, and we will come back once it is done
14. The installation is complete
    - ![Windows Server 2016 is now installed](img/VM3.png "Windows Server 2016 is now installed onto the Hyper-V VM")
    - Windows Server 2016 is now installed onto the Hyper-V VM
15. Let's check its network connection. We should be able to get out to the internet because we are using external switch for this VM
    - I am going to use ipconfig to check my IP address and try to ping google.com to see if it is successful
    - ![Pulling network information](img/VM_IP.png "Pulling network information")
        - It looks like this Hyper-V VM is joined to the YCFOREST domain
        - It is getting the same default gateway as my router and it is getting an IP address
        - Looks good
    - ![Pinging Google](img/VM_IP2.png "Pinging Google")
        - It can ping to Google, so it can get to the internet
    - Looks like this Hyper-V VM is getting a proper IPv4 address and it is able to get out to the internet since it can successfully ping to Google
16.	Hyper-V set up complete


## *Hyper-V server and Hyper-V VM are both configured and functioning properly*