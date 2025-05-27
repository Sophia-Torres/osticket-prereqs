# 🧾 osTicket LAB – PREREQUISITES & INSTALLATION

This tutorial outlines the full environment setup for deploying **osTicket v1.15.8** on a **Windows 10 Virtual Machine in Microsoft Azure**. It includes installation of all dependencies, configuration steps, and guidance on preparing osTicket for use in a help desk simulation lab.

---

## 🔍 LAB OVERVIEW

osTicket is a widely-used open-source support ticket system that allows you to simulate the daily responsibilities of IT support analysts and administrators. In this lab, you'll build and configure your own support environment on a Windows 10 Azure VM using IIS, PHP, MySQL, and osTicket.

---

## 🧰 TECHNOLOGIES USED

- Microsoft Azure (Windows 10 VM)
- IIS (Internet Information Services)
- PHP 7.3.8
- MySQL 5.5
- osTicket v1.15.8
- PHP Manager for IIS
- URL Rewrite Module
- HeidiSQL (GUI for MySQL)

---

## ✅ PREREQUISITES

- Microsoft Azure account
- Remote Desktop (RDP) access (Now called Windows App on Mac)
- Basic knowledge of Windows and web services

---

## 🖥️ VIRTUAL MACHINE CONFIGURATION

| Setting     | Value                |
|-------------|----------------------|
| Name        | `osticket-vm`        |
| OS          | Windows 10           |
| vCPUs       | 4                    |
| Username    | `labuser`            |
| Password    | `osTicketPassword1!` |

<img width="842" alt="image" src="https://github.com/user-attachments/assets/805bc6e2-da22-41b7-9c93-32b040e300bc" />


---

## 📂 Setup Instructions

### 1. 🔑 Connect to Your VM
- Add your vm to Remote Desktop using its public IP address 
- Log in as **labuser**

### 2. 📦 Download Installation Files
- Download `osTicket-Installation-Files.zip`
- Unzip to Desktop → Folder: `osTicket-Installation-Files`

### 3. 🌐 Install IIS with CGI Enabled
- Go to **Control Panel > Programs > Turn Windows features on/off**
- Enable:
  - World Wide Web Services
    - Application Development Features → ✅ CGI
  - Web Management Tools →  ✅ IIS Management Console

![image](https://github.com/user-attachments/assets/6d2b41d4-08ef-4505-b12d-9d6fb0824035)

<img width="436" alt="image" src="https://github.com/user-attachments/assets/c40ec337-3c25-459f-beb0-66a3d3c594b4" />



---

### 4. ⚙️ Install Dependencies

- From `osTicket-Installation-Files` folder, install:
  - ✅ PHP Manager for IIS (`PHPManagerForIIS_V1.5.0.msi`)
  - ✅ URL Rewrite Module (`rewrite_amd64_en-US.msi`)
  - ✅ VC++ Redistributable (`VC_redist.x86.exe`)

- Create folder: `C:\PHP`

- Extract `php-7.3.8-nts-Win32-VC15-x86.zip` into `C:\PHP`

- Install MySQL 5.5:
  - File: `mysql-5.5.62-win32.msi`
  - Type: **Typical Setup**
  - Standard configuration
  - Root user: `root`
  - Password: `root`

  <img width="519" alt="image" src="https://github.com/user-attachments/assets/9573bf78-8c0a-434a-8a72-af785e96ae68" />


---

### 5. 🧩 Configure IIS and PHP

- Open **IIS Manager** as Administrator  
- Use **PHP Manager** to register: `C:\PHP\php-7.3.8-nts-Win32-VC15x86\php-cgi.exe`  

<img width="952" alt="image" src="https://github.com/user-attachments/assets/87a6bf89-1f1a-4e0e-aaff-45e66af686f5" />

- Restart IIS: Stop and Start server

---

### 6. 📥 Install osTicket

- Extract `osTicket-v1.15.8.zip`  
- Copy the `upload` folder into: `C:\inetpub\wwwroot`  
- Rename `upload` → `osTicket`  

- Reload IIS
- Go to Sites → Default Web Site → osTicket
- In right pane click Browse *:80
  
![image](https://github.com/user-attachments/assets/936f3648-90bd-48c7-a6c0-4c41e07e6ca0)

- osTicket should open in your browser


---

### 7. 🔧 Enable PHP Extensions

In PHP Manager > Enable Extensions:
- ✅ `php_imap.dll`  
- ✅ `php_intl.dll`  
- ✅ `php_opcache.dll`  

Refresh browser to confirm changes

![image](https://github.com/user-attachments/assets/e4f6fc8f-38b5-46ba-9626-acce238e9104)


---

### 8. 🛡️ Configure osTicket

- Rename config file:  
  `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php` →  
  `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

- Set permissions for file by right clicking and selecting properties → Clicking Security → Clicking Advanced:
  - Disable inheritance
  - Remove all
  - For Lab purposes, add new permission:
    - User/Group: `Everyone`
    - Permission: `Full Control`

  <img width="810" alt="image" src="https://github.com/user-attachments/assets/910bf6d6-1a7a-41d8-86fa-99993160171c" />


---

### 9. 🧑‍💻 Complete Web Setup

- Open `http://localhost/osTicket` in browser
- Set:
  - System Settings
  - Admin User
 <img width="1141" alt="image" src="https://github.com/user-attachments/assets/c9663125-72b9-4fdd-8ed7-5c2db394db1b" />


---

### 10. 🗃️ Create MySQL Database

- Go back into the osTicket-Installation-Files
- Install HeidiSQL

<img width="826" alt="image" src="https://github.com/user-attachments/assets/f6755b1c-a788-42cf-9061-a8ca0298b332" />

- Connect using:
  - Username: `root`
  - Password: `root`
- Create new database: `osTicket`

![image](https://github.com/user-attachments/assets/ac0d3dbc-4a96-40aa-8441-276990cf5802)

Return to browser and complete setup:
- Database Name: `osTicket`
- MySQL User: `root`
- Password: `root`

Click **Install Now!**

<img width="1030" alt="image" src="https://github.com/user-attachments/assets/93cd302c-97de-4eff-b5d1-b965ef0ba4e5" />


---

## Links we will use for [Post-Installation Configuration](https://github.com/Sophia-Torres/osticket-postinstall)

- Admin Portal:  
  `http://localhost/osTicket/scp/login.php`

- End User Portal:  
  `http://localhost/osTicket/`



