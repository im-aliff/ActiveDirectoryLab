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
   2. At the top-right corner, click `Manage`, then click `Add Roles and Features`.
   3. Click `Next`, and make sure that the `Role-based or feature-based installation` radio button is selected, click `Next`, then click `Next` again.
   4. Click on `Active Directory Domain Services`, then click on `Add features`, click `Next` until you see `Install`, then click `Install`.
   5. After installation has been completed, close the window.

4. **Promote to Domain Controller**:
   1. In the `Server Manager` window, click the flag icon that is beside `Manage`, and click the blue `Promote this server to a domain controller` text.
   2. Click the `Add a new forest` radio button to create a brand-new domain, and type in whatever name you want, followed by a `.` and some text (such as the word `local`) in the text box next to the `Root domain name:` text, and click `Next`.
   3. Leave all options as default, in the `Password:` field, type in a good password, then in the `Confirm password:` field, re-enter your password, then click `Next` until you see the `Install` option, then click `Install`.
   4. Once the installation is completed, the machine will automatically restart.
   5. Go to log in to the Windows Server 2022 machine, and if you notice `Domain\Administrator`, it means you have successfully installed Active Directory Domain Services, and that this machine has been successfully promoted to a Domain Controller.

### Step 2: Set Up Windows 10 PC

1. **Install Windows 10**:
   - Boot from the installation media and follow the on-screen instructions to install Windows 10.
![image](https://github.com/user-attachments/assets/49647c1d-9a84-487c-8493-e642c80d3889)

2. **Change Hostname to `target-PC`**:
   - Follow the same steps as for changing the server name:
     1. In the Windows taskbar, search for `PC`, click `Properties`, then click the `Rename this PC` button.
     2. Type in `target-PC`, click `Next`, then click `Restart now`.

3. **Join Windows 10 to the Domain**:
   - Right-click on `This PC` and select `Properties`.
   - Click on `Change settings` next to the computer name.
   - Click `Change` and select `Domain`, then enter the domain name (e.g., `example.com`).
   - Provide domain administrator credentials to join the domain and restart the computer.

### Step 3: Create Organizational Units and Users

1. **Create Organizational Units**:
   - Open `Active Directory Users and Computers` on the Domain Controller.
   - Right-click on the domain name (e.g., `example.com`), select `New`, and then `Organizational Unit`.
   - Create OUs named `IT` and `HR`.

2. **Add Users**:
   - Right-click on the `IT` OU, select `New`, and then `User`.
   - Enter the user details for Jenny Smith (username: `jsmith`).
   - Repeat the process for the `HR` OU to create a user for Terry Smith (username: `tsmith`).

## Usage

### Managing Users

- **Reset Password**:
  - Open `Active Directory Users and Computers`.
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
