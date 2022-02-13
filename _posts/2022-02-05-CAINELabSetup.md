---
layout: post
title: Forensics Virtual Lab with CAINE
categories: [Tutorials]
tag: [forensics] 
---

I will be showcasing how to setup CAINE for a virtual Forensics lab. CAINE is a great tool for digital forensics as it comes pre-packaged with tools such as Autopsy and Volatility. Also I will do a quick demo following the training "Forensic Analysis: Network Incident Response" by ENISA (https://www.enisa.europa.eu/topics/trainings-for-cybersecurity-specialists/online-training-material/technical-operational/#Forensic_analysis_Network_Incident_Response).


## Requirements

For this setup, you will need the following:
- CAINE iso (https://www.caine-live.net/)
- VirtualBox (https://www.virtualbox.org/)
- An evidence drive (Example: http://enisa.europa.eu/ftp/ENISA-Ex2-Evidence.vmdk)

## Setup 

*You don't have to install CAINE since normally you would use it live but it'll make things faster for exercises within a virtual environment.*

If you do install CAINE inside a VM then you may encounter a problem with GRUB. To fix the GRUB bootloader issue, please follow the tutorial at `https://www.youtube.com/watch?v=atHr2OGCQiQ&t=1s&ab_channel=CyberEntirety`

Other than that you should be able to boot up your CAINE VM with ease. You may want to change the display resolution to suit your screen. Alternatively, you can install the virtualbox guest additions which automatically adjusts the screen resolution for you.

If you have installed CAINE, make sure you take a snapshot of your CAINE VM after your setup. 
## Demo 

For this demo I will be using an image from ENISA's training website on "Forensic Analysis: Network Incident Response" (link provided in the [Requirements](#requirements)) 

### Preparing the evidence drive

Before booting up your CAINE VM, you need to add the evidence vmdk drive as a storage device in the CAINE VM settings.

![CAINE VM Storage Settings](../../assets/img/cainelab/caine-vm-settings.png)
_Figure 1: CAINE VM Storage Settings_

Boot up and login to your CAINE VM. Next thing you'll need to do is mount the evidence image. The *safest* way to mount an evidence drive is by using the `Mounter` utility in CAINE on the bottom right of the taskbar; this makes sure the device is mounted in read-only to avoid corrupting the drive.

![Evidence Mount](../../assets/img/cainelab/caine-mount.png)
_Figure 2: Evidence Mount_

Alternatively, you can mount the connected drive through the commands:
```bash
lsblk # to check if device is in sdb1 (it should be by default)
sudo mount /dev/sdb1 
```


Now that we have the evidence drive mounted, we'll copy the `pfsense` and `dhcpsrv` directories to our CAINE VM.
```bash
# Create empty directory 
cd ~/Desktop/
mkdir forensic-demo && cd forensic-demo
# Copy directories to current directory
cp -r /media/sdb1/pfsense ./
cp -r /media/sdb1/dhcpsrv ./
```

### Collecting network evidence

### Network forensic analysis

