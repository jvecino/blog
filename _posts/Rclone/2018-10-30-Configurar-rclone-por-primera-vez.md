---
layout: default
title:  "Como configurar rclone por primera vez"
categories: rclone
---

# Como configurar rclone por primera vez
* * *

## Instalación rclone

Para instalar rclone en linux/macOS/BSD:

```
curl https://rclone.org/install.sh | sudo bash
```

Para instalar la beta:
```
curl https://rclone.org/install.sh | sudo bash -s beta
```

Para los demás sistemas operativos nos vamos al mirror en github:

```
https://github.com/ncw/rclone/releases/tag/v1.44
```

log:

``````
user@ubuntu:~$ sudo curl https://rclone.org/install.sh | sudo bash
[sudo] password for user:
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4178  100  4178    0     0  10527      0 --:--:-- --:--:-- --:--:-- 10523
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    13  100    13    0     0     34      0 --:--:-- --:--:-- --:--:--    34
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 8481k  100 8481k    0     0  11.7M      0 --:--:-- --:--:-- --:--:-- 11.7M
Archive:  rclone-current-linux-amd64.zip
   creating: tmp_unzip_dir_for_rclone/rclone-v1.44-linux-amd64/
  inflating: tmp_unzip_dir_for_rclone/rclone-v1.44-linux-amd64/rclone.1  [text]                                                                                                                                                              
  inflating: tmp_unzip_dir_for_rclone/rclone-v1.44-linux-amd64/rclone  [binary]
  inflating: tmp_unzip_dir_for_rclone/rclone-v1.44-linux-amd64/README.txt  [text                                                                                                                                                             ]
  inflating: tmp_unzip_dir_for_rclone/rclone-v1.44-linux-amd64/README.html  [tex                                                                                                                                                             t]
 extracting: tmp_unzip_dir_for_rclone/rclone-v1.44-linux-amd64/git-log.txt  [emp                                                                                                                                                             ty]
Purging old database entries in /usr/share/man...
Processing manual pages under /usr/share/man...
Purging old database entries in /usr/share/man/fr...
Processing manual pages under /usr/share/man/fr...
Purging old database entries in /usr/share/man/sv...
Processing manual pages under /usr/share/man/sv...
Purging old database entries in /usr/share/man/fi...
Processing manual pages under /usr/share/man/fi...
Purging old database entries in /usr/share/man/pt_BR...
Processing manual pages under /usr/share/man/pt_BR...
Purging old database entries in /usr/share/man/cs...
Processing manual pages under /usr/share/man/cs...
Purging old database entries in /usr/share/man/id...
Processing manual pages under /usr/share/man/id...
Purging old database entries in /usr/share/man/zh_TW...
Processing manual pages under /usr/share/man/zh_TW...
Purging old database entries in /usr/share/man/da...
Processing manual pages under /usr/share/man/da...
Purging old database entries in /usr/share/man/it...
Processing manual pages under /usr/share/man/it...
Purging old database entries in /usr/share/man/zh_CN...
Processing manual pages under /usr/share/man/zh_CN...
Purging old database entries in /usr/share/man/hu...
Processing manual pages under /usr/share/man/hu...
Purging old database entries in /usr/share/man/ko...
Processing manual pages under /usr/share/man/ko...
Purging old database entries in /usr/share/man/ru...
Processing manual pages under /usr/share/man/ru...
Purging old database entries in /usr/share/man/de...
Processing manual pages under /usr/share/man/de...
Purging old database entries in /usr/share/man/es...
Processing manual pages under /usr/share/man/es...
Purging old database entries in /usr/share/man/nl...
Processing manual pages under /usr/share/man/nl...
Purging old database entries in /usr/share/man/sl...
Processing manual pages under /usr/share/man/sl...
Purging old database entries in /usr/share/man/tr...
Processing manual pages under /usr/share/man/tr...
Purging old database entries in /usr/share/man/pt...
Processing manual pages under /usr/share/man/pt...
Purging old database entries in /usr/share/man/pl...
Processing manual pages under /usr/share/man/pl...
Purging old database entries in /usr/share/man/ja...
Processing manual pages under /usr/share/man/ja...
Processing manual pages under /usr/local/man...
Updating index cache for path `/usr/local/man/man1'. Wait...done.
Checking for stray cats under /usr/local/man...
Checking for stray cats under /var/cache/man/oldlocal...
1 man subdirectory contained newer manual pages.
1 manual page was added.
0 stray cats were added.
0 old database entries were purged.

rclone v1.44 has successfully installed.
Now run "rclone config" for setup. Check https://rclone.org/docs/ for more details.

user@ubuntu:~$
```

## Configuración de nuestra primera cuenta
```
user@ubuntu:~$ rclone config
```

```
user@ubuntu:~$ rclone config
2018/10/30 09:25:59 NOTICE: Config file "/home/user/.config/rclone/rclone.conf" not found - using defaults
No remotes found - make a new one
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
name> miconexion
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
12 / Google Drive
   \ "drive"

Storage> 12
** See help for drive backend at: https://rclone.org/drive/ **

Google Application Client Id
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_id>
Google Application Client Secret
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_secret>
Scope that rclone should use when requesting access from drive.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / Full access all files, excluding Application Data Folder.
   \ "drive"
 2 / Read-only access to file metadata and file contents.
   \ "drive.readonly"
   / Access to files created by rclone only.
 3 | These are visible in the drive website.
   | File authorization is revoked when the user deauthorizes the app.
   \ "drive.file"
   / Allows read and write access to the Application Data folder.
 4 | This is not visible in the drive website.
   \ "drive.appfolder"
   / Allows read-only access to file metadata but
 5 | does not allow any access to read or download file content.
   \ "drive.metadata.readonly"
scope> 1
ID of the root folder
Leave blank normally.
Fill in to access "Computers" folders. (see docs).
Enter a string value. Press Enter for the default ("").
root_folder_id>
Service Account Credentials JSON file path
Leave blank normally.
Needed only if you want use SA instead of interactive login.
Enter a string value. Press Enter for the default ("").
service_account_file>
Edit advanced config? (y/n)
y) Yes
n) No
y/n> n
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine or Y didn't work
y) Yes
n) No
y/n> n
If your browser doesn't open automatically go to the following link: https://accounts.google.com/o/oauth2/auth?access_type=offline&
Log in and authorize rclone for access
Enter verification code> 4/hgC5DFGDF4Gp7RKGrV98L_iZPwPblM
Configure this as a team drive?
y) Yes
n) No
y/n> n
--------------------
[miconexion]
type = drive
scope = drive
token = {"access_token":"ya29.GltGBv5vYJ_Vx8Y80cdfg5GF6rAt1Yj23FzrjUw7ciis5Ptl7z99KVXvtXfxLwE0jduhPh-j","token_type":"Bearer","refresh_token":"1/1bscXCzKgh59P5CjnvhHCnExjq-mxFfhw06uM_VghqQPoCWNQflb","expiry":"2018-10-30T10:26:48.927281425+01:00"}
--------------------
y) Yes this is OK
e) Edit this remote
d) Delete this remote
y/e/d> y
Current remotes:

Name                 Type
====                 ====
miconexion           drive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q
```
