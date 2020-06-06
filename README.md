sap-preconfigure-assert
=======================

This role checks if a RHEL 7 or RHEL 8 system has been set up according to applicable SAP notes so that SAP business software can be installed.

Requirements
------------

None.

Role Variables
--------------

- set in `defaults/main.yml`:

### Perform only certain checks of SAP notes
If the following variable is set to no, only certain steps of SAP notes will be checked as per setting of variable `sap_preconfigure_assert_<sap_note_number>_<step>`. If this variable is undefined or set to no, all steps of applicable SAP notes will be checked.
```yaml
sap_preconfigure_assert_config_all
```

### Define configuration steps of SAP notes
For defining one or more steps of SAP notes to be executed or checked only, set variable `sap_preconfigure_assert_config_all` to `no` and one or more of the following variables to `yes`:
```yaml
sap_preconfigure_assert_2002167_0[2...6], example: sap_preconfigure_assert_2002167_03
sap_preconfigure_assert_1391070
sap_preconfigure_assert_2772999_[02...10], example: sap_preconfigure_assert_2772999_10
```

### Minimum package check
The following variable will check if packages are installed at minimum required versions as defined in files `vars/*.yml`. Default is `yes`.
```yaml
sap_preconfigure_assert_min_package_check
```

### How to behave if reboot is required
The following variable will ensure that the role will fail if a reboot is required, if undefined or set to `yes`, which is also the default. By setting the variable to `no`, the role will not fail if a reboot is required.
```yaml
sap_preconfigure_assert_fail_if_reboot_required
```

### Define SELinux state
The following variable allows for defining the desired SELinux state. Default is `disabled`.
```yaml
sap_preconfigure_assert_selinux_state
```

### Perform a yum update
- This function is currently not implemented -
If the following variable is set to `yes`, the role will check if a `yum update` will update any software on the managed node. Default is `no`. \
*Note*: The outcome of a `yum update` depends on the managed node's configuration for sticky OS minor version, see the description of the release option in `man subscription-manager`. For SAP HANA installations, setting a certain minor version with `subscscription-manager release --set=X.Y` is a strict requirement.
```yaml
sap_preconfigure_assert_update
```

### size of TMPFS in GB:
The following variable contains a formula for setting the size of TMPFS according to SAP note 941735.
```yaml
sap_preconfigure_assert_size_of_tmpfs_gb
```

### Locale
The following variable contains the locale to be check. This check is currently not implemented.
```yaml
sap_preconfigure_assert_locale
```

### Check /etc/hosts
If you not want the role to check `/etc/hosts` according to SAP's requirements, set the following variable to `no`. Default is `yes`.
```yaml
sap_preconfigure_assert_modify_etc_hosts
```

### hostname
If the role should not use the hostname as reported by Ansible (=`ansible_hostname`), set the following variable according to your needs:
```yaml
sap_hostname
```

### DNS domain name
If the role should not use the DNS domain name as reported by Ansible (=`ansible_domain`), set the following variable according to your needs:
```yaml
sap_domain
```

### IP address
If the role should not use the primary IP address as reported by Ansible (=`ansible_default_ipv4.address`), set the following variable according to your needs:
```yaml
sap_ip
```

### Linux group name of the database user
The following variable contains the name of the group which is used for the database(s), e.g. dba.
```yaml
sap_preconfigure_assert_db_group_name
```

Dependencies
------------

This role does not depend on any other role.

Example Playbook
----------------

```yaml
---
    - hosts: all
      roles:
         - role: sap-assert-preconfigure
         - role: sap-hana-assert-preconfigure
```

Example Usage
-------------
ansible-playbook -l remote_host site.yml

License
-------

GNU General Public License v3.0

Author Information
------------------

Bernd Finger
