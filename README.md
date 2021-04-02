Role Name
=========

An Ansible role that install backup scripts with configuration for crypto backup from NFC to cloud via WebDav.

Requirements
------------

N/A

Role Variables
--------------

* `cloud_backup`: list of configuration for NFS, WebDav and CryFS
* `cloud_backup_configuration`: list of configuration for each backup

Each of `cloud_backup` and `cloud_backup_configuration` must have the same name of node.

Example configuration:
```
    cloud_backup:
        - name: MyBackup
          # NFS
          nfs_src: 192.172.1.1:/folder
          nfs_mount_path: nfs
          # DavFS
          davfs2_mount_path: davfs2
          davfs2_src: https://webdav.myserver.com
          davfs2_login: MyLogin
          davfs2_password: MyPassword
          # CryFS
          cryfs_mount_path: cryfs
    cloud_backup_configuration:
        - name: MyBackup
          # NFS
          nfs_mount_path: nfs
          # DavFS
          davfs2_mount_path: davfs2
          # CryFS
          cryfs_password: CryFsPath
          cryfs_basedir: TestBackup
          cryfs_mount_path: cryfs
          # Backup
          rsync_options: -a
          backup_source: SomeFolder
          cron:
              minute: 30
              hour: 2
              day: "*"
              month: "*"
              weekday: "*"
```

Note: You mast using Ansible Vault for store sensetive information like credential.

Dependencies
------------

N/A

Example Playbook
----------------

```
---
- name: Install backup script
  roles:
    - role: kirill_zak.ansible_davfs_cryfs_cloud_backup
```

License
-------

MIT

Author Information
------------------

https://kirill-zak.ru

Build status
------------

[![Build Status](https://travis-ci.com/kirill-zak/ansible-davfs-cryfs-cloud-backup.svg?branch=master)](https://travis-ci.com/kirill-zak/ansible-davfs-cryfs-cloud-backup)