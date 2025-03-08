Role Name
=========

freebsd-jails

Creates jail(s) on a FreeBSD host.

Requirements
------------

None.

Role Variables
--------------

# If true will pull the base from the internet
# If false it will pull from a local path
freebsd_jails_online_pull: false

# zfs dataset  to create on the host if using zfs
freebsd_jails_jails_path: zroot/jails

# jails base directory to create
freebsd_jails_jails_directory: /jails

# mountpoint to use if using zfs
freebsd_jails_jails_zfs_mountpoint: /jails

# directory where the base.txz files will be copied
freebsd_jails_jails_base_dir: base_tar_files

# where each release of the base.txz will copied
freebsd_jails_jail_folders:
  - dir_name: "{{ freebsd_jails_jails_directory }}/{{ freebsd_jails_jails_base_dir }}"
    owner: root
    group: wheel
    mode: "0700"

# holds some basic fail info. The url and src will be referenced
# based on the value of the freebsd_jails_testing variable.  if 
# true it will reference the src attribute, if false the url att-
# tribute will be referenced.
freebsd_jails_jailinfo:
  - name: my_jailname
    path: "{{ freebsd_jails_jails_directory }}/my_jailname"
    url: "{{ freebsd_jails_releases_online[0]['online_url'] }}"
    src: /mnt/nfs/priv/bsd/base/13.1/base.txz
    checksum: "{{ freebsd_jails_releases_online[0]['checksum'] }}"
    dest: "/root/{{ freebsd_jails_jails_base_dir}}/my_jailname/base.txz"
    ipv4_address: 172.16.20.100
    ipv6_address:
    nic: en0
    dns_resolver0:
    dns_resolver1:

# users to create in the jail; this should exist in a vault
freebsd_jails_users:
  - name:
    groups:
    password:


# vars file for freebsd-jails

freebsd_jails_default_algorithm: sha256

# checksums for supported base.txz files internet version
freebsd_jails_releases_online:
  - release: 13.1
    algorithm: sha256sum
    checksum: sha256:565baf7cf520cedfa01c5260f6a614b71c5e2b37ba3ee22e1342906548aa24ad 
    online_url: https://download.freebsd.org/ftp/releases/amd64/13.1-RELEASE/base.txz
  - release: 13.3
    algorithm: sha256sum
    checksum: sha256:d10531d663cee5efeb7d696ca84ce90adacd1fae14dd249628fb74da0c7c2820
    online_url: https://download.freebsd.org/ftp/releases/amd64/13.3-RELEASE/base.txz
  - release: 13.4
    algorithm: sha256sum
    checksum: sha256:8e13b0a93daba349b8d28ad246d7beb327659b2ef4fe44d89f447392daec5a7c
    online_url: https://download.freebsd.org/ftp/releases/amd64/13.4-RELEASE/base.txz
  - release: 14.1
    algorithm: sha256sum
    checksum: sha256:bb451694e8435e646b5ff7ddc5e94d5c6c9649f125837a34b2a2dd419732f347
    online_url: https://download.freebsd.org/ftp/releases/amd64/14.1-RELEASE/base.txz


# checksums for supported base.txz files local version
freebsd_jails_releases_local:
  - release: 13.1
    algorithm: sha256sum
    checksum: 565baf7cf520cedfa01c5260f6a614b71c5e2b37ba3ee22e1342906548aa24ad  base.txz
    online_url: https://download.freebsd.org/ftp/releases/amd64/13.1-RELEASE/abase.txz
  - release: 13.3
    algorithm: sha256sum
    checksum: d10531d663cee5efeb7d696ca84ce90adacd1fae14dd249628fb74da0c7c2820  base.txz
    online_url: https://download.freebsd.org/ftp/releases/amd64/13.3-RELEASE/base.txz
  - release: 13.4
    algorithm: sha256sum
    checksum: 8e13b0a93daba349b8d28ad246d7beb327659b2ef4fe44d89f447392daec5a7c  base.txz
    online_url: https://download.freebsd.org/ftp/releases/amd64/13.4-RELEASE/base.txz
  - release: 14.1
    algorithm: sha256sum
    checksum: bb451694e8435e646b5ff7ddc5e94d5c6c9649f125837a34b2a2dd419732f347  base.txz
    online_url: https://download.freebsd.org/ftp/releases/amd64/14.1-RELEASE/base.txz

# this will create the necessary host entries for a jail
freebsd_jails_host_entries:
  - hostline

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - name: freebsd-jails

License
-------

BSD

Author Information
------------------

streamline-it


