Ansible Role: molecule_libvirt
=========

The role creates / destroys VMs via KVM for testing of ansible roles. It is designed to be used in create and destroy 
phase of molecule tests. 

Requirements
------------

No requirements necessary. Role will setup kvm/qemu/libvirt on target host. Adding remote user on target host to user group 
"kvm" and "libvirt" manually and do reboot may be required.

Role Variables
--------------

Create and destroy requires a definition of VMs to be created/destroyed like:

```
molecule_yml:
    platforms:
        - name: ubuntu-2004-1
          os: ubuntu
          version: 2004
        - name: ubuntu-2004-2
          os: ubuntu 
          version: 2004
```

"name" must be unique among all VM Instances. "os" and "version" have to match keys of images from defaults/main.yml.
"molecule_yml.platforms" reflects a part of the molecule.yml scenario file and is instantiated automatically by the
molecule framework.

Dependencies
------------

Collection "community.libvirt" is used to communicate with kvm.

Example Playbook
----------------

Playbook will setup kvm/qemu/libvirt on localhost and start two VMs based on Ubuntu 20.04 cloud images.

    - hosts: localhost
      connection: local
      vars:
        molecule_yml:
          platforms:
            - name: ubuntu-2004-1
              os: ubuntu
              version: 2004
            - name: ubuntu-2004-2
              os: ubuntu 
              version: 2004
      tasks:
         - include_role:
             name: molecule_libvirt
             tasks_from: create.yml

License
-------

MIT

Author Information
------------------

Benjamin Goetz - Fraunhofer IPA
