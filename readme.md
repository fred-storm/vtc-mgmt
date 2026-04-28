# Project Notes:

##Purpose
    This project exist to make life a bit easier managing a fleet of Cisco Codecs with Ansible to cover gaps left by call manager and other applications.  All of these playbooks are utilizing the http api. 

## Requirements
    - Ansible
    - lxlm
    - Apache2
    -Community.utility.xml

## Playbooks

    ### Get info
        This playbook will get generic info from any unit in the inventory file.  It gathers codec type, software version, system name, and serial number.

    ### Update codecs
        These playbooks will upgrade a codecs software to the version in the label utillizing a file server local to the ansible runner.  In my case I am using an apache web server to complete this so update file must be uploaded to /var/www/html/vtc/firmware directory, or if another directory is used the url will need to be changed in the playbook.