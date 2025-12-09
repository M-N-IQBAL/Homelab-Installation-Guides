# Ubuntu Server Installation on VMware Workstation

## 1. Introduction

This guide walks you through installing **Ubuntu Server** on **VMware Workstation** in a homelab environment. It is ideal for learning, server practice, and lab-based testing.

You will need:

* Ubuntu Server ISO
* VMware Workstation installed
* Minimum required system resources
* (Optional) `open-vm-tools` for better VM integration

 

## 2. Prerequisites

* **[VMware Workstation](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion)** (any recent version)
* **Ubuntu Server ISO**
  Download from the official Ubuntu website: [https://ubuntu.com/download/server](https://ubuntu.com/download/server)
* **Minimum VM specifications:**

  * 2 GB RAM (4 GB recommended)
  * 2 CPU cores
  * 20 GB storage
  * UEFI firmware (recommended)

## 3. Create the Virtual Machine

1. Open **VMware Workstation**, go to the top tabs, open the **Home** tab, and click **Create a New Virtual Machine**
   ![alt text](image-1.png)

2. Select **Custom (advanced)** → **Next**
   ![alt text](image-2.png)

3. Keep default hardware compatibility → **Next**
   ![alt text](image-3.png)

4. Choose **Installer disc image (ISO)** → select your Ubuntu Server ISO → **Next**
   ![alt text](image-4.png)

5. Enter a VM name (example: **Ubuntu-server**) and choose a storage location → **Next**
   ![alt text](image-5.png)

6. Configure processor settings (2 cores recommended) → **Next**
   ![alt text](image-6.png)

7. Choose memory size:

   * 16 GB system RAM → assign **4 GB**
   * 8 GB system RAM → assign **2 GB**
     → **Next**
     ![alt text](image-7.png)

8. Select **NAT** as the network connection → **Next**
   ![alt text](image-8.png)

9. Keep recommended I/O controller and disk type → **Next**
   ![alt text](image-9.png)

10. Set disk type to **SCSI (Recommended)** → **Next**
    ![alt text](image-10.png)

11. Choose **Create a new virtual disk** → **Next**
    ![alt text](image-11.png)

12. Set disk size to **20 GB or more** → **Next**
    ![alt text](image-12.png)

13. Keep the default disk file that appears → **Next**
    ![alt text](image-13.png)

14. Check **Power on this virtual machine after creation** → **Finish**
    ![alt text](image-14.png)


## 4. Install Ubuntu Server

Follow the installation screens:

1. Select **Try or install Ubuntu Server**
   ![alt text](image-15.png)

2. Select your preferred language → press **Enter**
   ![alt text](image-16.png)

3. Choose your keyboard layout → press **Enter**
   ![alt text](image-17.png)

4. Select **Ubuntu Server** as the installation type

   * If the X mark appears, it is selected
     → press **Enter**
     ![alt text](image-18.png)

5. Network configuration:

   * DHCP is automatically enabled
     → press **Enter**
     ![alt text](image-19.png)

6. Leave proxy field empty → **Enter**
   ![alt text](image-20.png)

7. Keep default mirror settings → **Enter**
   ![alt text](image-22.png)

8. Storage configuration:

   * Keep defaults → **Enter**
     ![alt text](image-23.png)
     ![alt text](image-24.png)
     ![alt text](image-25.png)

9. Profile setup:

   * Create your username and password → **Enter**
     ![alt text](image-26.png)

10. Skip Ubuntu Pro → **Enter**
    ![alt text](image-27.png)

11. Enable **OpenSSH Server** if you want SSH access → **Enter**
    ![alt text](image-28.png)

12. Leave featured server snaps unselected → **Enter**
    ![alt text](image-29.png)

13. Wait for installation to complete
    ![alt text](image-31.png)

14. When **Reboot Now** appears, press **Enter**
    ![alt text](image-32.png)

15. If you see a message such as:
    `[FAILED] Failed unmounting cdrom.mount`
    Simply press **Enter** and continue to login
    ![alt text](image-21.png)
    ![alt text](image-30.png)

## 5. Post-Installation

1. Update your system:

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

   ![alt text](image-33.png)

2. Install VMware Tools:

   ```bash
   sudo apt install open-vm-tools -y
   ```

3. Reboot:

   ```bash
   sudo reboot
   ```

After reboot, your VM will have improved performance, better mouse handling, and proper virtualization support.

(Optional) You may take a clean snapshot.

 
