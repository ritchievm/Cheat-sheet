Checklist:
in advance:check wire connection virtual box

1. check if needed packages are installed: yum info "packagename)
    - libsemanage-python, samba, samba-client, samba-common
2. check if samba is running:  sudo systemctl status smb.service AND  sudo systemctl status nmb.service

3. check if firewall is running: sudo firewall-cmd --state
 - if not running: systemctl start name.service 
 
4. check if samba is allowed through firewall: sudo firewall-cmd --list-all
 - if not allowed: firewall-cmd --permanent -add-service=smb (and nmb)
 
5. check the configuration files:vi or cat
    - Samba: etc/samba.smb.conf
    - ftp: etc/vsftpd/vsftpd.conf
    - If changes made restart service: systemctl restart smbd




Get logs: journalctl -f (show latest and wait for changes)

get firewall state: sudo firewall-cmd --state

check status of service: sudo systemctl status SERVICENAME.service
    smb(authent and file transf),nmb(provides netbios)

add samba to firewall :firewall-cmd --permanent --zone=public --add-service=samba
                      :firewall-cmd --reload
                    
Get samba config and edit: vi /etc/samba/smb.conf
Get status of seboolean: getsebool -a | grep "boolname"
set status of seboolean: setsebool "boolname" on/off

SEBooleans
  -samba_export_all_ro (read only to all directies)
  -samba_export_all_rw (read write to all directories)
  -smbd_anon_write
  -samba_enable_home_dirs
  
Check permissions for shared folder: ls -l  

give permissions to user: chmod -R xxxx user/group
give ownership chmod -R

allow SELinux: chcon -R -t public_content_rw_t







sources: http://www.techbrown.com/samba-server-configuration-on-linux.html
