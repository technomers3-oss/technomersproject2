<pre>
Analysing Android App Permissions and Mobile Traffic

A.VERIFY
1.C:\Users\Admin>cd C:\Users\Admin\AppData\Local\Android\Sdk\emulator
2.C:\Users\Admin\AppData\Local\Android\Sdk\emulator>emulator -list-avds

B.SETUP PROXY
1.cd C:\Users\Admin\AppData\Local\Android\Sdk\platform-tools
2.adb devices
3.adb shell settings put global http_proxy 10.0.2.2:8080
4.adb shell settings get global http_proxy

C.SEND CERTIFICATE TO EMULATOR
1.C:\Users\Admin\AppData\Local\Android\Sdk\platform-tools>adb push C:\Users\Admin\Downloads\burpcer.der /sdcard/Download/

----------------------------------------------------------------------------------------------





Creating and Analyzing Disk Images Using dc3dd and Autopsy
A. OPEN TERMINAL
1.Ctrl + Alt + T

B. CREATE SAMPLE EVIDENCE
1.echo "Cybersecurity Lab Evidence" > evidence.txt
2.ls

C. IDENTIFY DISK PARTITION
1.lsblk

D. CREATE PRACTICE DISK IMAGE
1.dd if=/dev/zero of=practice_disk.dd bs=1M count=100

E. FORMAT / MOUNT DISK
1.mkfs.ext4 practice_disk.dd

F. CREATE FORENSIC IMAGE USING dc3dd
1.sudo dc3dd if=practice_disk.dd of=forensic_image.dd hash=md5 log=acquisition.log

G. VERIFY IMAGE AND LOG
1.ls -lh practice_disk.dd
2.cat acquisition.log

H. START AUTOPSY TOOL
1.autopsy

I. ACCESS AUTOPSY IN BROWSER
1.http://localhost:9999/autopsy

J. (INSIDE AUTOPSY - GUI STEPS, NOT COMMANDS)
1.Create New Case
2.Add Host
3.Add Image → Select:
4./home/kali/forensic_image.dd

K. OPTIONAL (USEFUL ADDITIONAL COMMANDS FOR ANALYSIS)
1.pwd
2.whoami
3.df -h
4.file forensic_image.dd
5.md5sum forensic_image.dd













------------------------------------------------------------------------------------
Testing IoT Device Security (Default Passwords & Open Ports)

A. DEPLOY VULNERABLE IoT SIMULATION (DOCKER)
docker run -d -p 8090:3000 --name juiceshop bkimminich/juice-shop
docker ps
docker logs juiceshop

B. ACCESS APPLICATION (VERIFY DEPLOYMENT)
http://localhost:8090

C. IDENTIFY HOST IP ADDRESS
On Windows (if applicable):
ipconfig


D. NETWORK SCANNING FROM KALI LINUX
nmap 10.39.169.126
nmap -sV 10.39.169.126
nmap -A 10.39.169.126

E. PORT + SERVICE ENUMERATION (ADVANCED)
nmap -p- 10.39.169.126
nmap -sC -sV 10.39.169.126
nmap --open 10.39.169.126

F. ACCESS IoT DASHBOARD FROM ATTACKER MACHINE
http://10.39.169.126:8090

G. TEST DEFAULT / WEAK CREDENTIALS (MANUAL)
Open browser → http://10.39.169.126:8090
Try common credentials:
admin / admin
admin / password
user / user

H. ANALYZE NETWORK TRAFFIC (BROWSER DEV TOOLS)
Open Browser → Press F12
Go to Network Tab
Reload page
Inspect HTTP requests












---------------------------------------------------------------------------------------------

LOG FILE ANALYSIS FOR INCIDENT DETECTION LAB

A. NAVIGATE TO LOG DIRECTORY
cd /var/log
ls

B. VIEW SUCCESSFUL LOGIN RECORDS
last

C. VIEW SYSTEM LOGS (FULL)
journalctl
journalctl | less

D. FILTER FAILED LOGIN ATTEMPTS
journalctl | grep "Failed"
journalctl | grep "Failed password"

E. VIEW SSH LOGIN ACTIVITY
journalctl | grep ssh

F. FILTER SYSTEM ERRORS
journalctl | grep -i error

G. ANALYZE APACHE LOGS
cd /var/log/apache2
ls
sudo less access.log

H. DETECT SUSPICIOUS WEB REQUESTS
grep "404" /var/log/apache2/access.log

I. VIEW PACKAGE ACTIVITY
less /var/log/dpkg.log

J. REAL-TIME LOG MONITORING
sudo journalctl -f

K. SIMULATE FAILED SSH LOGIN ATTACK
Install SSH Server
sudo apt install openssh-server -y

Start SSH Service
2. sudo service ssh start

Find IP Address
3. ip a

Generate Failed Logins
4. ssh fakeuser@localhost
5. ssh kali@localhost

L. ANALYZE FAILED LOGIN ATTEMPTS
journalctl | grep "Failed password"

M. EXTRACT SUSPICIOUS IP ADDRESS
journalctl | grep "Failed password" | awk '{print $11}'

N. COUNT FAILED ATTEMPTS PER IP
journalctl | grep "Failed password" | awk '{print $11}' | sort | uniq -c | sort -nr

O. ALTERNATIVE METHOD (FAILED LOGINS)
sudo lastb

P. CHECK RECENT LOG ACTIVITY
journalctl --since "10 minutes ago"

--------------------------------------------------------------------------------------













CYBER SECURITY LAB EXPERIMENT
Privacy Audit of Apps & Websites + Data Breach Analysis

--------------------------------------------------
A. INSTALL NODE.js & npm
--------------------------------------------------
sudo apt update
sudo apt install nodejs npm -y

--------------------------------------------------
B. INSTALL NATIVEFIER
--------------------------------------------------
sudo npm install -g nativefier

--------------------------------------------------
C. CREATE WHATSAPP DESKTOP APP
--------------------------------------------------
nativefier https://web.whatsapp.com
ls

--------------------------------------------------
D. RUN WHATSAPP DESKTOP
--------------------------------------------------
cd WhatsAppWeb-linux-x64
./WhatsAppWeb

--------------------------------------------------
E. LOGIN TO WHATSAPP
--------------------------------------------------
(Open mobile WhatsApp → Linked Devices → Scan QR code)

--------------------------------------------------
F. ANALYZE TRACKERS (EXODUS PRIVACY)
--------------------------------------------------
(Open browser)
https://reports.exodus-privacy.eu.org

--------------------------------------------------
G. START WIRESHARK CAPTURE
--------------------------------------------------
wireshark
(Select interface: eth0 / wlan0 → Start)

--------------------------------------------------
H. GENERATE NETWORK TRAFFIC
--------------------------------------------------
(Use WhatsApp Desktop: send messages, images, open chats)

--------------------------------------------------
I. APPLY WIRESHARK FILTERS
--------------------------------------------------
tls
dns

--------------------------------------------------
J. STOP WIRESHARK CAPTURE
--------------------------------------------------
(Click Stop in Wireshark)

--------------------------------------------------
K. OPEN FACEBOOK WEBSITE
--------------------------------------------------
(Open browser)
https://www.facebook.com

--------------------------------------------------
L. START BURP SUITE
--------------------------------------------------
burpsuite

--------------------------------------------------
M. CONFIGURE PROXY (BROWSER)
--------------------------------------------------
IP: 127.0.0.1
Port: 8080

--------------------------------------------------
N. ENABLE INTERCEPTION (BURP)
--------------------------------------------------
(Turn Intercept ON → Reload Facebook page)

--------------------------------------------------
O. ANALYZE TRAFFIC (BROWSER DEVTOOLS)
--------------------------------------------------
(Press F12 → Network tab)

--------------------------------------------------
P. CHECK EMAIL DATA BREACH
--------------------------------------------------
(Open browser)
https://haveibeenpwned.com


---------------------------------------------------------------------------------------













CONDUCTING A SECURITY AUDIT AND RISK ASSESSMENT

--------------------------------------------------
A. SYSTEM INFORMATION
--------------------------------------------------
1. Press Windows + R
2. msinfo32

--------------------------------------------------
B. CHECK WINDOWS UPDATES
--------------------------------------------------
1. start ms-settings:windowsupdate
2. usoclient StartScan

--------------------------------------------------
C. CHECK FIREWALL STATUS
--------------------------------------------------
1. control firewall.cpl
2. netsh advfirewall show allprofiles

--------------------------------------------------
D. CHECK ANTIVIRUS STATUS
--------------------------------------------------
1. start windowsdefender:
2. sc query WinDefend

--------------------------------------------------
E. CHECK PASSWORD & ACCOUNT SECURITY
--------------------------------------------------
1. start ms-settings:signinoptions
2. net user

--------------------------------------------------
F. CHECK INSTALLED APPLICATIONS
--------------------------------------------------
1. appwiz.cpl
2. wmic product get name,version

--------------------------------------------------
G. CHECK STARTUP PROGRAMS
--------------------------------------------------
1. taskmgr
2. shell:startup

--------------------------------------------------
H. CHECK NETWORK SECURITY
--------------------------------------------------
1. start ms-settings:network-status
2. ipconfig /all
3. netsh wlan show profiles

--------------------------------------------------
I. CHECK BROWSER SECURITY
--------------------------------------------------
(Manual – no direct command)
1. Open Chrome/Edge
2. Go to Settings → Privacy & Security

--------------------------------------------------
J. CHECK DATA BACKUP
--------------------------------------------------
1. start ms-settings:backup
2. wbadmin get status

--------------------------------------------------
K. OPTIONAL SYSTEM SECURITY CHECKS
--------------------------------------------------
1. sfc /scannow
2. chkdsk
3. netstat -ano

--------------------------------------------------
L. RESULT
--------------------------------------------------
(System audit completed; vulnerabilities identified and mitigation suggested)








CDN 
[https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/Experiment%20l2.pdf](https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/Experiment%20l2.pdf)


[https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/log%20files%20l2_compressed.pdf](https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/log%20files%20l2_compressed.pdf)

[https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/risk%20l2.pdf](https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/risk%20l2.pdf)


[https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/testing2%20l2.pdf](https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/testing2%20l2.pdf)


[https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/week-8%20l2_compressed.pdf](https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/week-8%20l2_compressed.pdf)



[https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/whatsapp%20l2_compressed.pdf](https://cdn.jsdelivr.net/gh/technomers3-oss/technomersproject2@main/whatsapp%20l2_compressed.pdf)
</pre>
