#How to Configure Active Directory on an AWS Virtual Machine

> 🔐 This guide walks you through setting up Active Directory (AD) on a Windows Server EC2 instance in AWS

---

## ✅ Step 1: Launch a Windows Server EC2 Instance

1. Sign in to [AWS Management Console](https://aws.amazon.com/console/).
2. Go to **EC2 → Launch Instance**.
3. Set instance name (e.g., `AD-DomainController`).
4. Select AMI:  
   - **Microsoft Windows Server 2019** or **2022 Base**
5. Choose instance type:  
   - Recommended: `t2.medium` or larger
6. Create/select key pair for RDP login.
7. Configure Network Settings:
   - Auto-assign Public IP: **enabled**
   - Security group ports to allow:
     - RDP (3389)
     - DNS (53)
     - LDAP (389)
     - Optional: HTTP/HTTPS

---

## ✅ Step 2: Connect to the Instance via RDP

1. Select the instance → **Connect → RDP Clien
2. Download the `.rdp` file and decrypt the Windows password using your `.pem` key
3. Connect using RDP and log in as Administrator

---

## ✅ Step 3: Rename the Computer

1. Open Server Manager
2. Click on Local Server → Computer Name
3. Rename to something like `AD-DC1` and restart

---

## ✅ Step 4: Install Active Directory Domain Services (AD DS)

1. Server Manager → **Add roles and features**
2. Role-based installation → select your server
3. Add the Active Directory Domain Services role
4. Accept all required features → Next → Install

---

## ✅ Step 5: Promote Server to a Domain Controller

1. After install → click Promote this server to a domain controller
2. Choose **Add a new forest** → name it (e.g., `corp.local`)
3. Set options:
   - DNS Server + Global Catalog
   - Set DSRM password
4. Continue and install → the instance will reboot

---

## ✅ Step 6: Verify AD Setup

1. Log back into the instance
2. Go to **Server Manager → Tools → Active Directory Users and Computers
3. Confirm your domain (e.g., `corp.local`) exists
4. Create a new Organizational Unit (OU) or user for testing

---

## 🧹 Cleanup 

- Terminate instance when done
- Delete security groups, EIPs, and other resources to avoid charges

---

