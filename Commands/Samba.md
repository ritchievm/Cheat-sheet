###Checklist Van Mele Ritchie:
0. in advance: Check wire connection virtual box

1. check if needed packages are installed: yum info "packagename)
    - libsemanage-python, samba, samba-client, samba-common,(vsftpd for ftp)

2. check if samba is running:  sudo systemctl status smb.service AND  sudo systemctl status nmb.service

3. check if firewall is running: sudo firewall-cmd --state
 - if not running: systemctl start name.service 
 
4. check if samba is allowed through firewall: sudo firewall-cmd --list-all
    - if not allowed: firewall-cmd --permanent --zone=public -add-service=samba
    - and reload firewall firewall-cmd --reload
 
5. check the configuration files:vi or cat
    - Samba: etc/samba.smb.conf
    - ftp: etc/vsftpd/vsftpd.conf
    - If changes made restart service: systemctl restart smbd
    ![samba.conf example](https://github.com/ritchievm/Cheat-sheet/blob/master/Commands/samba.conf.png)
    
6. check selinux booleans: getsebool -a |grep "boolname"
    - if wrong value: setsebool "boolname" value
    - SEBooleans
        - samba_export_all_ro (read only to all directies)
        - samba_export_all_rw (read write to all directories)
        - smbd_anon_write
        - samba_enable_home_dirs
7. Check the persmissions for the shares

Extra needed toolscommands/knowledge

Get logs: journalctl -f (show latest and wait for changes)

give permissions to user: chmod -R xxxx user/group
give ownership chmod -R

get SElinux settings on a share: stat --format="%a/%U/%G/%C" "sharename"
allow SELinux on share folder: chcon -R -t public_content_rw_t /srv/shares/

get groups and their members: cat /etc/group
