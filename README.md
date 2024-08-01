# Active Directory Setup and Management

## Introduction
This project demonstrates the setup and management of an Active Directory (AD) environment using a demo PC running Windows 10 and a Windows Server 2022 for Active Directory Domain Control. The project includes creating two organizations (IT and HR) and adding users Jenny Smith (jsmith) and Terry Smith (tsmith).

## Objectives
- Set up a Windows Server 2022 as an Active Directory Domain Controller.
- Join a Windows 10 PC to the Active Directory domain.
- Create organizational units (OUs) for IT and HR departments.
- Add users Jenny Smith (jsmith) and Terry Smith (tsmith) to their respective OUs.
- Demonstrate basic AD management tasks.

## Network Diagram
<img width="723" alt="Screenshot 2024-07-31 at 6 21 29 PM" src="https://github.com/user-attachments/assets/42b58b5f-9158-4a32-a00d-881d13a4f1e1">

## Prerequisites
- Windows Server 2022 installation media or ISO.
- Windows 10 installation media or ISO.
- Virtualization software (e.g., VirtualBox, VMware) or physical hardware for installation.
- Basic understanding of networking and system administration.

## Installation Steps

### A. Create Virtual Machines in VirtualBox
1. **Create 2 Different Virtual Machines**:
   - Create a Windows 10 machine (target-PC).
   - Create a Windows Server 2022 machine (Active Directory Domain Controller).
![Design](https://github.com/user-attachments/assets/1dbe5678-4886-42e2-8a40-fc16ed25b633)

2. **Create a NAT Network in VirtualBox**:
   - Open VirtualBox, go to `File` > `Preferences` > `Network` > `NAT Networks`.
   - Click the `+` icon to add a new NAT network.
   - Name the network `AD-Project` and set the IP range to `192.168.10.0/24`.
![image](https://github.com/user-attachments/assets/d723e97b-3cb9-4326-a883-429a3962b7a9)

![image](https://github.com/user-attachments/assets/b87ee161-caa8-43f4-a0f4-19fc80fa04d3)


3. **Configure Network Settings for Virtual Machines**:
   - For each virtual machine (Windows 10 and Windows Server 2022):
     - Click on the virtual machine, then click `Settings`.
     - Click on `Network`.
     - In the `Adapter 1` tab, click inside the `Attached to:` dropdown menu and choose `NAT Network`.
     - In the `Name` dropdown menu, select the NAT network `AD-Project` created in the previous step.
     - Click `OK`.
![image](https://github.com/user-attachments/assets/bb97aef5-e724-48fd-a6c8-71e39c29b49a)
![image](https://github.com/user-attachments/assets/bab14702-4417-4c87-bb66-a91a7f9e1e75)



### Step 1: Install Windows Server 2022 and Promote to Domain Controller

1. **Install Windows Server 2022**:
   - Boot from the installation media and follow the on-screen instructions to install Windows Server 2022.
   - Set up the network configuration and ensure the server has a static IP address.
     1. Hit the `Windows` key, type in `cmd`, and hit `Enter`.
     2. In the command prompt, type `ipconfig` and hit `Enter` to check the IP address.
     3. At the right end of the taskbar, right-click the `network` icon and click `Open Network & Internet settings`.
     4. Scroll down and click on `Change adapter options`, right-click the network adapter, and click on `Properties`.
     5. Double-click `Internet Protocol Version 4 (TCP/IPv4)`, and click the `Use the following IP address:` radio button.
     6. In the `IP address` field, type in `192.168.10.7`, in the `Subnet mask` section, type in `255.255.255.0`, and in the `Default gateway` section, type in `192.168.10.1`.
     7. In the `Preferred DNS server:` section, type in `8.8.8.8`, then click `OK`, and close the window.
     8. In the command prompt, enter `ipconfig` to verify that the IPv4 Address is `192.168.10.7`.

2. **Change Hostname to `ADDC01`**:
   1. In the Windows taskbar, search for `PC`, click `Properties`, then click the `Rename this PC` button.
   2. Type in `ADDC01`, click `Next`, then click `Restart now`.
      
![image](https://github.com/user-attachments/assets/48d7e477-8e82-47d3-9287-e2a4e76d5635)

3. **Set Up Active Directory**:
   1. Hit the `Windows` key, click on `Windows Administrative Tools`, and click on `Server Manager`.
![image](https://github.com/user-attachments/assets/54d68795-525e-4f3e-a1f5-9c4c4ea350f8)

   2. At the top-right corner, click `Manage`, then click `Add Roles and Features`.
![Screenshot 2024-07-31 145228](https://github.com/user-attachments/assets/8b3785cd-0db3-423e-992d-dc67862ceb1d)
![Screenshot 2024-07-31 145304](https://github.com/user-attachments/assets/85c355d8-b87c-411e-a7e6-6036e854448b)
![Screenshot 2024-07-31 145440](https://github.com/user-attachments/assets/f5d55fbd-48b7-4ede-9feb-bdb14157b007)
   4. Click `Next`, and make sure that the `Role-based or feature-based installation` radio button is selected, click `Next`, then click `Next` again.
![Screenshot 2024-07-31 145551](https://github.com/user-attachments/assets/77b8c57f-2d65-454c-b1e5-8b130810f486)
   5. Click on `Active Directory Domain Services`, then click on `Add features`, click `Next` until you see `Install`, then click `Install`.
![Screenshot 2024-07-31 145732](https://github.com/user-attachments/assets/05d9c573-0b09-4fd0-b174-4d5c0f9db6f2)

   6. After installation has been completed, close the window.

4. **Promote to Domain Controller**:
![Screenshot 2024-07-31 145847](https://github.com/user-attachments/assets/7dbf9be1-076d-4b47-8273-5b4b1dfb46af)

   1. In the `Server Manager` window, click the flag icon that is beside `Manage`, and click the blue `Promote this server to a domain controller` text.
![Screenshot 2024-07-31 145927](https://github.com/user-attachments/assets/2f44ccfa-eadd-414a-9b19-c33688af037a)
![Screenshot 2024-07-31 150014](https://github.com/user-attachments/assets/2f37b0ea-1f7f-48b4-a91e-5d97f8ccd1d7)

   2. Click the `Add a new forest` radio button to create a brand-new domain, and type in whatever name you want, followed by a `.` and some text (such as the word `local`) in the text box next to the `Root domain name:` text, and click `Next`.
![Screenshot 2024-07-31 151136](https://github.com/user-attachments/assets/392eaf65-191a-4d23-85d1-2a72b10dbcfb)

   3. Leave all options as default, in the `Password:` field, type in a good password, then in the `Confirm password:` field, re-enter your password, then click `Next` until you see the `Install` option, then click `Install`.
![Screenshot 2024-07-31 151609](https://github.com/user-attachments/assets/03a96edd-cf01-4b7e-8ada-d3c75123ff5b)

   4. Once the installation is completed, the machine will automatically restart.
![Screenshot 2024-07-31 151949](https://github.com/user-attachments/assets/512d8da8-f66b-4a9e-8b15-b74e9e11211d)

   5. Go to log in to the Windows Server 2022 machine, and if you notice `Domain\Administrator`, it means you have successfully installed Active Directory Domain Services, and that this machine has been successfully promoted to a Domain Controller.

1. **Install Windows 10**:
   - Boot from the installation media and follow the on-screen instructions to install Windows 10.
   - Set the static IP address for Windows 10 (target-PC):
     1. Hit the `Windows` key, type in `cmd`, and hit `Enter`.
     2. In the command prompt, type `ipconfig` and hit `Enter` to check the IP address.
     3. At the right end of the taskbar, right-click the `network` icon and click `Open Network & Internet settings`.
     4. Scroll down and click on `Change adapter options`, right-click the network adapter, and click on `Properties`.
     5. Double-click `Internet Protocol Version 4 (TCP/IPv4)`, and click the `Use the following IP address:` radio button.
     6. In the `IP address` field, type in `192.168.10.100`, in the `Subnet mask` section, type in `255.255.255.0`, and in the `Default gateway` section, type in `192.168.10.1`.
     7. In the `Preferred DNS server:` section, type in `8.8.8.8`, then click `OK`, and close the window.
     8. In the command prompt, enter `ipconfig` to verify that the IPv4 Address is `192.168.10.100`.

![image](https://github.com/user-attachments/assets/49647c1d-9a84-487c-8493-e642c80d3889)

2. **Change Hostname to `target-PC`**:
   - Follow the same steps as for changing the server name:
     1. In the Windows taskbar, search for `PC`, click `Properties`, then click the `Rename this PC` button.
     2. Type in `target-PC`, click `Next`, then click `Restart now`.

3. **Join Windows 10 to the Domain**:
   - Right-click on `This PC` and select `Properties`.
![Screenshot 2024-07-31 155634](https://github.com/user-attachments/assets/fa185e68-fb2c-45de-8735-d34551fa45d0)

![Screenshot 2024-07-31 155726](https://github.com/user-attachments/assets/3521aa94-c4de-4a83-b929-fb380f30520d)

   - Click on `Change settings` next to the computer name.
![image](https://github.com/user-attachments/assets/957f3d0b-1bd7-47e2-9b44-7bc7b766de91)

   - Click `Change` and select `Domain`, then enter the domain name (e.g., `xplore.local`).
![Screenshot 2024-07-31 155940](https://github.com/user-attachments/assets/93b65bc5-c58c-41e0-b52b-a1cf352ea5ee)
![Screenshot 2024-07-31 160310](https://github.com/user-attachments/assets/996c3fbd-9d5e-430b-9efd-e4f7f2dc5e92)
![Screenshot 2024-07-31 160429](https://github.com/user-attachments/assets/748ba076-089b-4637-80ff-64ad5ca81be1)

     FYI: There will be an error due to DNS server which is set to 8.8.8.8, We need to change it to 192.168.10.7 under network and connection.
![Screenshot 2024-07-31 160723](https://github.com/user-attachments/assets/666d90aa-cdd6-46e1-a979-a2ccb3b05549)
![Screenshot 2024-07-31 160901](https://github.com/user-attachments/assets/e055b7fb-9e9a-465b-a152-e3658fc1a7a3)

   - Provide domain administrator credentials to join the domain and restart the computer.

### Step 3: Create Organizational Units and Users

1. **Create Organizational Units**:
![Screenshot 2024-07-31 152240](https://github.com/user-attachments/assets/11d59ff1-76a3-427e-9fce-d9dcb4582ba8)

   - Open `Active Directory Users and Computers` on the Domain Controller.
![Screenshot 2024-07-31 153152](https://github.com/user-attachments/assets/e1ed2042-9e13-4b49-80a7-b4613ca84d3e)

   - Right-click on the domain name (e.g., `xplore.local`), select `New`, and then `Organizational Unit`.
![Screenshot 2024-07-31 153330](https://github.com/user-attachments/assets/21150649-b87d-4865-aa35-dac311c38f35)

   - Create OUs named `IT` and `HR`.

2. **Add Users**:
![Screenshot 2024-07-31 153408](https://github.com/user-attachments/assets/0ce68507-a73f-4062-b31d-fed24c43a64d)

   - Right-click on the `IT` OU, select `New`, and then `User`.![Screenshot 2024-07-31 153611](https://github.com/user-attachments/assets/134f88d9-1a6c-4a70-a6b3-352242260589)
![Screenshot 2024-07-31 153750](https://github.com/user-attachments/assets/31645225-0db3-4ad4-917b-689dd07ebf1e)
![Screenshot 2024-07-31 153830](https://github.com/user-attachments/assets/78fb9efa-7ced-4337-8ebe-016a783a0e0e)

   - Enter the user details for Jenny Smith (username: `jsmith`).
![Screenshot 2024-07-31 154204](https://github.com/user-attachments/assets/fe247cdf-94f2-4a7c-bb4f-9e4ba00db4af)

   - Repeat the process for the `HR` OU to create a user for Terry Smith (username: `tsmith`).

## Usage

### Managing Users

- **Reset Password**:
  - Open `Active Directory Users and Computers`.
![Screenshot 2024-07-31 153750](https://github.com/user-attachments/assets/d06228e5-9159-4bb2-ac16-770b7fc9f80b)


  - Navigate to the user (e.g., `jsmith`), right-click, and select `Reset Password`.
  - Enter and confirm the new password.

- **Move User to Another OU**:
  - Open `Active Directory Users and Computers`.
  - Drag and drop the user (e.g., `jsmith`) to the desired OU.

### Common AD Tasks

- **Create Groups**:
  - Right-click on an OU, select `New`, and then `Group`.
  - Enter the group name and configure its scope and type.

- **Assign Users to Groups**:
  - Right-click on a group, select `Properties`, and then `Members`.
  - Click `Add` and enter the usernames to add them to the group.

## Contributing
Feel free to fork this repository and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.

## License
This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.
