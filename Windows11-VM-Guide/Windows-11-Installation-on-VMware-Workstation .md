# **Windows 11 Installation on VMware Workstation 25H2**


## **1. Introduction**

This guide walks you through installing Windows 11 on VMware Workstation 25H2 in a lab environment.
It is designed for learning, testing, and homelab setups.

You will need:

* A Windows 11 ISO
* VMware Workstation installed
* Minimum required system resources
* (Optional) VMware Tools for better VM performance

---

## **2. Prerequisites**

* [VMware Workstation 25H2](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion)
* Windows 11 ISO (from the official [Microsoft website](https://www.microsoft.com/en-us/software-download/windows11))
* Minimum VM specifications:

  * 4 GB RAM (8 GB recommended)
  * 2 CPU cores
  * 64 GB disk space
  * UEFI enabled
  * TPM 2.0

---

## **3. Create the Virtual Machine**

1. Open VMware Workstation and click **Create a New Virtual Machine**
   ![alt text](images/1.png)

2. Choose **Typical (Recommended)** and click *Next*

   ![alt text](images/2.png)

3. Select **Hardware Compatibility** and click *Next*

   ![alt text](images/3.png)

4. Choose **Installer disc image (ISO)** → browse to your Windows 11 ISO → *Next*
   ![alt text](images/4.png)

5. Enter a VM name such as `Windows11-Lab`, choose a storage location with enough free space → *Next*
   ![alt text](images/5.png)

6. Configure encryption as required → *Next*

   ![alt text](images/6.png)

7. Set firmware type to **UEFI (Recommended)** → *Next*

   ![alt text](images/7.png)

8. Configure processor settings according to your CPU (multiple cores recommended) → *Next*
   ![alt text](images/8.png)

9. Choose memory size.

   * If you have 16 GB system RAM: assign 8 GB
   * If you have 8 GB system RAM: assign 4 GB
     → *Next*

     ![alt text](images/9.png)

10. Select **NAT** as the network connection → *Next*

    ![alt text](images/10.png)

11. Select the recommended I/O controller and disk type → *Next*

<table>
<tr>
<td>

![alt text](images/11.png)

</td>
<td>

![alt text](images/12.png)

</td>
</tr>
</table>

12. Choose **Create a new virtual disk** → *Next*

    ![alt text](images/13.png)

13. Keep recommended disk size (64 GB), select disk file location → *Next*

    ![alt text](images/14.png)

14. Check **Power on this virtual machine after creation** → *Finish*

    ![alt text](images/16.png)

---

## **4. Install Windows 11**

Follow the on-screen setup steps:

1. Select your preferred **language** and **keyboard layout**

2. Click **Install Windows 11**
   On the product key screen, click **I don’t have a product key**

<table>
<tr>
<td>

![alt text](images/19.png)

</td>
<td>

![alt text](images/20.png)

</td>
</tr>
</table>

3. Select **Windows 11 Pro** → *Next*
   Accept the license agreement
   ![alt text](images/21.png)

4. On the installation location screen, select the disk and click **Next**, then **Install**

<table>
<tr>
<td>

![alt text](images/23.png)

</td>
<td>

![alt text](images/24.png)

</td>
</tr>
</table>

5. Wait for Windows setup to complete
6. Go through the out-of-box experience (OOBE)
7. After logging in, Windows will load — though not in full screen yet
   ![alt text](images/35.png)

---

## **5. Post-Installation (VMware Tools)**

Install VMware Tools for improved graphics, mouse integration, and full-screen resolution.

1. In VMware Workstation, click **VM → Install VMware Tools**
   ![alt text](images/36.png)

2. A pop-up will appear inside the VM. Open it and start the setup:
   ![alt text](images/38.png)
   ![alt text](images/39.png)
   ![alt text](images/40.png)

3. After installation, reboot the VM.
   You should now have full-screen display and smooth performance.
   ![alt text](images/41.png)

4. (Optional) Take a clean snapshot.

---

# **Install Sysmon**

1. Inside the Windows 11 VM, download [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)

   Extract the downloaded ZIP file and open the folder:
   ![alt text](images/download.png)

2. Download the Sysmon Modular [config](https://raw.githubusercontent.com/olafhartong/sysmon-modular/refs/heads/master/sysmonconfig.xml) (by Olaf Hartong) 
   

   Save this file **inside the same Sysmon folder**.

3. Open PowerShell **as Administrator** inside that folder.

4. Install Sysmon:

```
.\Sysmon64.exe -accepteula -i .\sysmonconfig.xml
```

5. Confirm that Sysmon is running:

```
Get-Service Sysmon64
```

> Note: If you used a different configuration file name, update the command accordingly.

6. Verify Sysmon events:

```
Get-WinEvent -LogName Microsoft-Windows-Sysmon/Operational | Select-Object -First 10
```

![alt text](images/sysmon-cmd.png)

You can also confirm through Event Viewer:

`Applications and Services Logs > Microsoft > Windows > Sysmon > Operational`

![alt text](images/sysmonn.png)

At this point, your Windows 11 VM is fully set up with Sysmon running.

---
