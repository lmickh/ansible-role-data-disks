data-disks
=========

Format disks, create software devices, and manage mount unit files for systemd.

Assumes whole disk is used for a single mount point.

Intended to handle standard, lvm, and mdadm devices. mdadm device support is
in progress.

Requirements
------------

- Ansbile ~> 2.4
- systemd
- blkid
- lvm
- mdadm
- parted

Role Variables
--------------

```
data_disks:
  - path: /opt/standard_example
    devices: ['/dev/sdc']        # Only list single device for 'standard' disks
    type: standard               # Defaults to 'standard' if left undefined
    fs_type: xfs
    fs_options:                  # Optional
      - su=512
      - sw=128
    mount_options:               # Optional
      - noatime
      - nobarrier
  - path: /opt/lvm_example
    devices: ['/dev/sdd', '/dev/sde']
    fs_type: xfs
    type: lvm
    lvm_vg: vg_appdata
    lvm_lv: lv_data1
    lvm_size: 100%VG             # Optional
    lvm_vg_options: '--clustered n' # Optional
    lvm_lv_options: ''           # Optional
    lvm_pesize: 4                # Optional
```

Dependencies
------------

No role dependencies

Example Playbook
----------------
```
    - hosts: some_servers
      vars:
        data_disks:
          - path: /opt
            devices: ['/dev/sdc']
            fs_type: xfs
      roles:
        - {{ lmickh.data-disks}}
```

License
-------

MIT
