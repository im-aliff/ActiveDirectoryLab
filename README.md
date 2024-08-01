# Active Directory Setup and Management

## Introduction
This project demonstrates the setup and management of an Active Directory (AD) environment using a demo PC running Windows 10 and a Windows Server 2022 for Active Directory Domain Control. The project includes creating two organizations (IT and HR) and adding users Jenny Smith (jsmith) and Terry Smith (tsmith).

## Objectives
- Set up a Windows Server 2022 as an Active Directory Domain Controller.
- Join a Windows 10 PC to the Active Directory domain.
- Create organizational units (OUs) for IT and HR departments.
- Add users Jenny Smith (jsmith) and Terry Smith (tsmith) to their respective OUs.
- Demonstrate basic AD management tasks.
##Network Diagram
<img width="723" alt="Screenshot 2024-07-31 at 6 21 29 PM" src="https://github.com/user-attachments/assets/42b58b5f-9158-4a32-a00d-881d13a4f1e1">

## Prerequisites
- Windows Server 2022 installation media or ISO.
- Windows 10 installation media or ISO.
- Virtualization software (e.g., VirtualBox, VMware) or physical hardware for installation.
- Basic understanding of networking and system administration.
![Design](https://github.com/user-attachments/assets/1dbe5678-4886-42e2-8a40-fc16ed25b633)


## Installation Steps

### Step 1: Install Windows Server 2022 and Promote to Domain Controller

1. **Install Windows Server 2022**:
   - Boot from the installation media and follow the on-screen instructions to install Windows Server 2022.
   - Set up the network configuration and ensure the server has a static IP address.

2. **Promote to Domain Controller**:
   - Open Server Manager.
   - Add the `Active Directory Domain Services` (AD DS) role.
   - Follow the prompts to promote the server to a Domain Controller, creating a new forest and domain (e.g., `example.com`).

### Step 2: Set Up Windows 10 PC

1. **Install Windows 10**:
   - Boot from the installation media and follow the on-screen instructions to install Windows 10.

2. **Join Windows 10 to the Domain**:
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
