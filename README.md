data-disks
=========

Format disks, create software devices, and manage mount unit files for systemd.

Assumes whole disk is used for a single mount point.

Intended to handle standard, lvm, and mdadm devices. mdadm device support is
in progress.

Requirements
------------

Ansbile ~> 2.4
systemd
blkid
lvm
mdadm
parted

Role Variables
--------------

data_disks:
  - path: /opt/example
    devices: ['/dev/sdc']        # Only list single device for 'standard' disks
    type: standard               # Defaults to 'standard' if left undefined
    fs_type: xfs
    fs_options:
      - su=512
      - sw=128
    mount_options:
      - noatime
      - nobarrier
  - path: /opt/data1
    devices: ['/dev/sdd']
    type: lvm
    fs_type: xfs


Dependencies
------------

No role dependencies

Example Playbook
----------------

    - hosts: some_servers
      vars:
        data_disks:
          - path: /opt
            devices: ['/dev/sdc']
            fs_type: xfs
      roles:
        - {{ lmickh.data-disks}}

License
-------

MIT
