# Deploying_Windows_In_Proxmox
Deploying a Windows operating systems on the PROXMOX hypervisor

Summary:
---
So this took a little time to figure out, and a big shout out to @redpillcybersecurity, their walkthrough helped smooth out the issues I ran into during initial setup. So if your looking at adding a Windows operating system onto your PROXMOX home lab, read below.

Tools Used:
---
- Proxmox
- VirtIO driver ISO
- Windows Flavor ISO

body:
---
1. We need to ensure our ISO files are uploaded to our repository inside PROXMOX, please see following [guide](placeholderImportISOIntoPROXMOX) if not already setup.

2. We also need drivers to help us complete the installation, these can be retrieved from: https://pve.proxmox.com/wiki/Windows_VirtIO_Drivers you can click the "download latest stable" link in the installation section of the article to get the latest and greatest from RedHat. After downloading go ahead and import them into our repository.

3. Let's create the VM, select the Create VM button at the top right.

4. We run through the VM creation wizard, and on the OS tab we need to select not only our windows.iso but also check the "add additional drive for VirtIO drives" checkbox and select the downloaded drivers from our local repository. The next few tabs are up to you and what you want to allow, recourses wise, for your VM.

<img width="1306" height="999" alt="Screenshot 2025-10-21 095308" src="https://github.com/user-attachments/assets/5f3a6e83-1090-4b3f-b7de-ac439eb30a42" />


5. After you wrap that all up we should have a nice new windows VM ready for boot and install. in my case I've created a Windows 10 VM.

<img width="373" height="270" alt="Screenshot 2025-10-21 113947" src="https://github.com/user-attachments/assets/109f63b3-adac-44f2-9196-a51d23acfbda" />


6. I like to use SPICE as my display, i find it a smoother experience and if you need help setting this up on your system you can follow my quick [guide](placeholder-setupspiceviewer).

<img width="1778" height="425" alt="Screenshot 2025-10-21 095529" src="https://github.com/user-attachments/assets/0dcd49ef-2783-428b-ac76-0480062d3185" />


7. Now we can hit the start button near the top right cluster of buttons.

<img width="588" height="100" alt="Screenshot 2025-10-21 112932" src="https://github.com/user-attachments/assets/b1bfc257-08cf-4301-bf67-56f1a43fb1d4" />

8. For me i ran into an issue where the VM was having network connectivity issues and not booting to the windows install page, I went into the machine components and removed the "media" that housed the drivers, rebooted the machine and there was a small windows that stated to "press any key" before it booted back to the connectivity issue. So...with another reboot i jammed at the keyboard and the system switched to the blue screen of installing.

<img width="1264" height="850" alt="Screenshot 2025-10-21 100049" src="https://github.com/user-attachments/assets/0455f015-1554-47f5-8f20-d5b00f6b49b4" />


9. From here we jam that next button until  you reach the select a drive to install page, you will not see a drive here but there is where the VirtIO drivers come into play. So in my case i needed to go back to my hardware section of the VM and reselect the drivers.iso. 

<img width="1461" height="604" alt="Screenshot 2025-10-21 113407" src="https://github.com/user-attachments/assets/c3992c1d-f523-4bf5-9529-a80a3e0feab3" />


10. Then back at the install page we want to browse through our disk drive that houses our drivers, navigate to the following path:  vioscsi/w10/amd64 (or your OS version). after selecting that adm64 file press ok and then the drive space we allocated should pop up.

<img width="1282" height="867" alt="Screenshot 2025-10-21 100620" src="https://github.com/user-attachments/assets/e6b8b53e-6d02-4119-9e2d-02e9fde8c0e6" />

<img width="1274" height="859" alt="Screenshot 2025-10-21 100738" src="https://github.com/user-attachments/assets/78b152ac-0fc5-42a6-b9fb-a7d0bb860a0d" />

11. Then walk through the install process and you should be able to boot into windows. After that I went through the device manager, looked up any issues with drivers and then used that same driver.iso drive to install the latest for any hardware that deeded it.



Resources:
- https://pve.proxmox.com/wiki/Windows_VirtIO_Drivers
- https://www.youtube.com/watch?v=gC6iU4Msu6s&t=1135s
- 
