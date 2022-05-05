---
layout: post
title:  "Solution to fix USB showing incorrect capacity"
date:   2022-05-04 00:00:00 +0900
image:  '/assets/img/solution_to_usb_wrong_size/cover.jpg'
tags:   [tech, repair, usb]
---

Recently I encountered a situation where my usb shows only a very small amount in its capacity (roughly ~30KB !!!).

![wrong_size.png](/assets/img/solution_to_usb_wrong_size/wrong_size.png)

After researched, I found a solution and the steps can be achieved below:

# Using Windows
To fix this issue, we are going to use **Command Prompt** on Windows

Open the **Start Menu**, search for **Command Prompt**, right-click on it when you see it in the results, and select Run as administrator.

If you are using Windows 10, You can open **Powershell** as well.

Once the **Command Prompt** is opened, type the following command and hit Enter. It’ll launch the command-line version of the Disk Utility program.

**diskpart**
![disk_part.png](/assets/img/solution_to_usb_wrong_size/disk_part.png)

Type in the following command to view all the disks attached to your computer. Your USB drive will be one of these disks.

**list disk**
![list_disk.png](/assets/img/solution_to_usb_wrong_size/list_disk.png)

To perform an operation on your drive, run the following command replacing N with the actual number for your USB drive.

**select disk N**
![select_disk.png](/assets/img/solution_to_usb_wrong_size/select_disk.png)

Use the following command to clean up your USB drive.

**clean**
![clean.png](/assets/img/solution_to_usb_wrong_size/clean.png)

<image 4>

When the drive is cleaned, run the following command to create new partitions.

**create partition primary**
![create_partition.png](/assets/img/solution_to_usb_wrong_size/create_partition.png)


Finally, use the following command to format the drive to FAT32 format.
(or to NTFS if you replace `fs=fat32` to `fs=ntfs`)

**format fs=fat32 quick**
![format.png](/assets/img/solution_to_usb_wrong_size/format.png)

Once your drive is formatted, it's recommended to unplug it and then plug it back into your computer. 
<br />You’ll then find that your computer allows you to use the full storage capacity of your drive.

![correct_size.png](/assets/img/solution_to_usb_wrong_size/correct_size.png)