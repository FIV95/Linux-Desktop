# Linux PC Setup & Configuration (EndeavourOS)

## **1. Introduction**
This document outlines the process taken to set up and configure an EndeavourOS-based Linux PC for non-technical users. The primary goals of this setup were **security, automation, usability, and stability** while ensuring a familiar Windows-like experience.

This document does **not** include discussions about optimizing the ONN tablet, which is handled separately.

---

## **2. Initial Setup & System Installation**
### **2.1 Installing EndeavourOS**
- Downloaded the EndeavourOS ISO from the official website.
- Created a bootable USB drive using `balenaEtcher`.
- Booted into the Live Environment and installed EndeavourOS using the graphical installer.
- Selected **Cinnamon** as the Desktop Environment due to user familiarity with older Windows versions.
- Allowed the installation to complete and rebooted into the new system.

### **2.2 First Boot & System Updates**
After installation, the following steps were taken to ensure the system was up to date:
- Ran the system update command:
  ```bash
  sudo pacman -Syu
  ```
- Confirmed successful update completion before proceeding with further configurations.

---

## **3. Security & Stability Enhancements**
### **3.1 Checking System Status**
- Verified the system was running correctly post-installation.
- Checked that all hardware components (WiFi, graphics, peripherals) were recognized and functioning.

### **3.2 Ensuring Safe Package Management**
- Enabled the **multilib repository** (for additional compatibility with 32-bit applications):
  ```bash
  sudo nano /etc/pacman.conf
  ```
  - Uncommented the `[multilib]` section.
  - Saved changes and ran:
    ```bash
    sudo pacman -Syu
    ```

- Installed essential utilities for ongoing management:
  ```bash
  sudo pacman -S base-devel git curl wget htop
  ```

### **3.3 Implementing Automatic System Updates**
- **Created Bash scripts** for automating updates and maintenance.
- Set up a **cron job** to run these scripts periodically:
  ```bash
  crontab -e
  ```
  - Added a cron job for automatic system updates:
    ```
    0 3 * * 0 /usr/local/bin/system-maintenance.sh
    ```

---

## **4. USB Security & Data Transfer**
A USB drive containing documents and Microsoft-format contacts was introduced. The following steps were taken to ensure security before accessing the files:

### **4.1 Scanning the USB for Potential Threats**
- **Before opening any files**, the USB was checked for security risks.
- Installed **ClamAV** to scan the drive for malware:
  ```bash
  sudo pacman -S clamav
  sudo freshclam
  sudo clamscan -r /mnt/usb
  ```
- No significant threats were detected, allowing the next step of transferring data.

### **4.2 Data Extraction & Organization**
- The **USB was mounted manually** before transferring files:
  ```bash
  sudo mkdir /mnt/usb
  sudo mount /dev/sdb1 /mnt/usb
  ```
- **Scanned and removed confidential information** manually before transferring the necessary files.
- Copied the cleaned files to the appropriate directories on the system.

---

## **5. Contact Conversion**
### **5.1 Converting Windows XML Contacts to CSV Format**
- The contacts from the USB were originally in **Windows-specific XML format**.
- Successfully converted them into a **CSV format**, making them readable in LibreOffice.

- **LibreOffice was installed** to inspect and manipulate `.csv` files:
  ```bash
  sudo pacman -S libreoffice-fresh
  ```

---

## **6. Enhancing Usability for Non-Technical Users**
### **6.1 Installing Essential Software**
To make the system more user-friendly, the following applications were installed:
- **Web Browser:**
  ```bash
  yay -S librewolf-bin
  ```
- **Email Client:**
  - No standalone email client was installed as **Proton Mail Web Client** was used instead.
- **Office Suite:**
  ```bash
  sudo pacman -S libreoffice
  ```
- **File Manager (GUI-Based) for Easy Navigation:**
  ```bash
  sudo pacman -S thunar
  ```
- **Password Manager & VPN:**
  ```bash
  yay -S protonvpn-cli proton-pass
  ```

### **6.2 Configuring Quick-Access Auto-Launch VPN**
- Set up **ProtonVPN** to automatically connect for free-roam website navigation.
- Ensured VPN starts at boot with a quick-access toggle for ease of use.

### **6.3 Writing a User Guide**
- Created a **troubleshooting guide** for common issues and basic system operations.
- Included step-by-step instructions for **using ProtonVPN, navigating files, and basic system recovery steps**.

---

## **7. Conclusion**
The **EndeavourOS-based Linux PC was successfully set up and configured** with a focus on stability, usability, and security. Key highlights include:
- **Installation of Cinnamon for a familiar Windows-like experience.**
- **Successful conversion of Windows XML contacts to CSV.**
- **Implementation of Bash scripts & cron jobs for automated system updates.**
- **Use of Proton VPN for secure, quick-access web browsing.**
- **Creation of a troubleshooting guide to assist non-technical users.**

With these implementations, the system is now fully operational and optimized for daily use.

