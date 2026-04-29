# Project Notes:

## Purpose
This project exist to make life a bit easier managing a fleet of Cisco Codecs with Ansible to cover gaps left by call manager and other applications.  All of these playbooks are utilizing the http api. 

## Requirements
- Ansible
- lxlm
- Apache2
- Community.utility.xml

## Playbooks

### Get info
This playbook will get generic info from any unit in the inventory file.  It gathers codec type, software version, system name, and serial number.

### Update codecs
These playbooks will upgrade a codecs software to the version in the label utillizing a file server local to the ansible runner.  In my case I am using an apache web server to complete this so update file must be uploaded to /var/www/html/vtc/firmware directory, or if another directory is used the url will need to be changed in the playbook. * *Web server managment is outside the scope of this project.* *

#### Code Model Codes
- rkm = room kit mini
- rkp = room kit pro
- rk = room kit
- dskp = desk pro
- dsk = desk

## Syslog Settings
This playbook is setting all of the required settings to push syslogs and audit logs to external servers.  I am using it to push to Splunk, but there could be other uses for this as well.

## LDAP Settings
This one sets all of the requirements to use LDAP for administrator log ins.  This playbook specificaly is utilizing LDAPS and sAMAccountName to perform the query.

## Notes
Use the moduel_defaults block at the playbook definition to avoid laying out the full url at ever api call. Example in test-xml.yml

There are step upgrades needed when updating codecs from CE 9.x versions. The two step upgrades are:
- CE 9.15.6
- CE 10.19.5

If you are coming from behind any of these step upgrades you **MUST** step otherwise the codec will not accept the new file on upload.

## Info Needed for comparison
- [ ] At RoomOs 11.20.2 Bind DN and Bind PW now exist in ldap configuration. Does this exist in lower versions? When introduced?
- [ ] Do codecs older than 11.17 return the following feilds in /Status/SystemUnit?
    - Product ID
    - Software.DisplayName
    - BroadcastName
    - Hardware.Module.SerialNumber
