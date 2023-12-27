# Blog on Windows Server 2019 lab set up

## YCFOREST domain set up


### This is a github repo that contains the blog of my process of learning to set up my Windows Server forest in my computer

## Troubleshooting
##### These will document my struggles in the project and what I did to fix the issue as well as what I learned from troubleshooting

**[Troubleshooting](troubleshooting/README.md)**

## Processes of setting up:

1. [Installing VMWare Workstation and setting up Windows Server 2019](step_1/README.md "My initial configuration")
    - Installing and configuring VMWare Workstation
    - Create a Windows Server Virtual Machine and install Windows Server 2019 on it using the Windows Server 2019 ISO
    - Configure the network and settings of the initial VM

2. [Set up and deploy the first domain controller](step_2/README.md "My Primary domain controller configuration")
    - Rename the server to be WIN2K19-DC01 and set up the static IP address for the server
    - Give the add the active directory roles and services
    - Create a new domain called YCFOREST and promote the server to be the domain controller of the domain
    - Set up DNS services 

3. [Set up and deploy secondary domain controller](step_3/README.md "My secondary domain controller configuration")
    - Create a new domain controller by creating a installing a new VM
    - Set up the network static IP address for the VM and name it WIN2K19-DC02
    - Add the active directory roles and services and promote it to be the domain controller of the domain
    - Set up DNS services

4. [Set up and deploy Read Only Domain Controller](step_4/README.md "My Read Only Domain Controller configuration")
    - Create a new domain controller by creating a installing a new VM
    - Set up the network static IP address for the VM and name it WIN2K19-RODC01
    - Add the active directory roles and services and set it up so that the domain controller can only have read only permissons in the domain
    - Set up DNS services

5. [Set up and deploy child domain](step_5/README.md "Child domain configuratoin")
    - Create a new VM and set up the IP address. Name it WIN2K19-CDC01
    - Create a child domain in the forest, and make this machine the domain controller of the child domain
    - Add a client machine to the child domain active directory

6. [Set up and configure Windows Server Core](step_6/README.md "Windows Server Core configuration")
    - Install the Windows Server 2019 Core edition, set up the static IP address and name it WIN2K19-Core
    - Join the server to the domain
    - Configure the server settings

7. [Set up and configure file server to the domain](step_7/README.md "File server configuration")
    - Set up and install a new VM and set up the static IP address. Name it WIN2K19-FS01
    - Add the file server role to the server
    - Create the share drive and test it client machines in the domain

8. [Set up and configure DHCP services to the primary domain controller](step_8/README.md "DHCP service configuration")
    - Add the DHCP role in the primary domain controller
    - Configure the DHCP settings and create address pools
    - Create reserved addresses for future uses

9. [Set up and configure iSCSI target server](step_9/README.md "iSCSI configuration")
    - Add a iSCSI configuration to the file server
    - Set up the virtual disk for the iSCSI shares
    - Configure the iSCSI target and initiator server

10. [Set up and configure Windows Deployment Server](step_10/README.md "Windows Deployment Server configuration")
    - Set up and install a new VM and set up the static IP address. Name it WIN2K19-WDS01
    - Add the Windows Deployment Server role to the server
    - Configure PXE set ups for Windows 10 and Windows Server 2019
    - Do test deployments on virtual machines

11. [Set up and configure Windows Update Service to the domain](step_11/README.md "WSUS configuration")
    - Set up and install a new VM and set up the static IP address. Name it WIN2K19-WSUS01
    - Add the Windows Update Service role to the server
    - Configure the WSUS service to sync and deploy updates to the servers in the domain

12. [Set up and configure print server to the domain](step_12/README.md "Print server configuration")
    - Add the print and document services to the file server
    - Configure print and document services in the server
    - Add printer drivers to the print and document services to set up print service in the domain

13. [Set up and configure FTP server to the domain](step_13/README.md "FTP server configuration")
    - Set up and install a new VM and set up the static IP address. Name it WIN2K19-FTP01
    - Add the IIS FTP role to the server
    - Configure and set up the FTP service in the domain and test it in a client machine using FileZilla

14. [Set up and configure distrubuted file server to the domain](step_14/README.md "DFS configuration")
    - Set up and install a new VM and set up the static IP address. Name it WIN2K19-DFS01
    - Add the distrubuted file server namespace and replication role to the server
    - Create and configure the DFS namespaces and test it using client machines in the domain

15. [Set up and configure DFS relication](step_15/README.md "My P2 README.md file")
    - Set up and install a new VM and set up the static IP address. Name it WIN2K19-DFS02
    - Add the Distrubuted File Server namespace and relication role to the server
    - Create, configure, and test replication group

16. [Set up and configure Hyper-V server to the domain](step_16/README.md "My P2 README.md file")
    - Set up and install a new VM and set up the static IP address. Name it WIN2K19-HPV01
    - Add the Hyper-V role to the VM
    - Set up Hyper-V and create a virtual machine within the Hyper-V server
    - Set up the VM within the Hyper-V server and join it to the domain

17. [Set up and configure Hyper-V replication to the domain](step_17/README.md "My P2 README.md file")
    - Set up and install a new VM and set up the static IP address. Name it WIN2K19-HPV02
    - Add the Hyper-V role to the domain
    - Configure Hyper-V replication and failover settings with the first Hyper-V server(WIN2K19-HPV01)
    - Test the sync and failover to see if the VM in HPV01 will copy or fail over to HPV02

