# 🐧 Linux Automated Backup Script

## 💡 Project Overview
This project demonstrates how to create a **Linux Bash backup script** that automatically stores files in a separate folder with the current date (`YYYY-MM-DD`). 

The script is designed to provide **safety** in case of accidental file loss or data breaches. Companies or organizations can easily back up their files every day by running a simple command.

---

## ✨ Features
* **Automatic Timestamping:** Automatically creates a timestamped backup directory (`/Backup/YYYY-MM-DD`).
* **Secure Copy:** Copies all confidential files from `/Confidential` into the daily backup folder.
* **Folder Handling:** Handles folder creation if the directory does not exist.
* **Single Command Execution:** Can be executed with a single command.

---

## 🛠️ Skills Demonstrated
* **Bash scripting**
* Linux file system management
* **Automation** of repetitive tasks
* Basic **cybersecurity** awareness (backup and disaster recovery)

---

## ⚙️ How It Works
1.  **Check for Backup Directory:** The script checks for the existence of the current day's directory. If it doesn’t exist, the script creates `/Backup/YYYY-MM-DD`.
2.  **Copy Files:** Recursively copies all files from `/Confidential` into the newly created or existing backup directory.
3.  **Completion Message:** Displays a success or warning message when the backup is done.

---

## ✅ Prerequisites
* Linux system with **Bash**
* **Root or sudo privileges** (if necessary to access folders)
* A source folder, `/Confidential`, containing the files to back up

---

## 📜 Script Usage

### 1. Create the Script (`Backup.sh`)

Use `sudo nano Backup.sh` to create the file and paste the following content:

```bash
#! /bin/bash
#Creating a Script that will backup confidential files from "/Confidential" folder into the "/Backups" folder together with current <date> equal with <current_date>

#Storing the current date 
date=$(date +%F)
echo "current date read as: $date"

if [ ! -d "/Backups/$date" ]
then
        echo "/Backups/$date does not exists, creating directory"
        mkdir "/Backups/$date"
else
        echo "Warning: /Backups/$date already exist, backup will overwrite"
fi

#Copying confidential files from "/Confidential" folder into "/Backups" folders
cp -r home/vboxuser/Desktop/Confidential/* /Backups/$date/
```
---

## ⏰ Automating the Backup with Cron
To make the backup fully automatic, schedule the script to run every day at a specific time using cron.

### 1. Open the root user's crontab
```bash
sudo crontab -u root -e
```
* [Editing Crontab](Screenshots/Running_Scrip_2_Crontab.png)

---

## 2. Add the following line to schedule the backup
```bash
2 14 * * * /opt/Backup.sh
```

---

## Explanation
| Field | Value | Meaning |
| :--- | :--- | :--- |
| **Minute** | `2` | Runs at minute 2 of the hour |
| **Hour** | `14` | Runs at 14:00 (2 PM) |
| **Day of Month** | `*` | Runs every day of the month |
| **Month** | `*` | Runs every month |
| **Day of Week** | `*` | Runs every day of the week |

## 🚀 Result
Cron will now automatically execute the script every 24 hours, ensuring daily backups without manual input.

---

## 📸 Screenshots
* [Editing Script](Screenshots/Editing_Script_Screenshoot_1.png)
* [Running Script](Screenshots/Running_Script_2.png)
* [Backup Folder](Screenshots/Backup_Folder_3.png)


