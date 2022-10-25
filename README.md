(Opinionated) Linux Defaults
=========

Highly opinionated defaults for Linux systems.

Shell support is BASH only for now. Currently optimized for Debian, Fedora is a WIP.

I am open to making changes or improvements as longs as they make sense to me and suit my purposes. Feel free to fork.

Requirements
------------

No specific requirements at this time.

Role Variables
--------------

```yaml
default_timezone: 'America/Chicago' # Sets the time zone on the server.
default_shell: bash                 # Sets which shell to configure, if you want a different one, be sure to add it to the installed packages.
ssh_well_known_hosts:               # Does not include defaults. Array of hosts that should have their host keys imported to be trusted.
  - github.com
  - gitlab.com
default_packages:                   # Array of packages to install, defaults are defined per system, see vars/*.yaml
bash_aliases:                       # Array of Dicts of aliases to install for bash. Defaults are defined per system in vars/*.yaml
  - name: ls
    command: ls -lah
global_users:                       # Array of users to create on every host.
          - name: username
            pass: P@$$w0rd1         # Plain text password, will be salted and hashed
            authorized_keys:
              - "key_1"
              - "key_2"
            sudo: bool
        host_users:                 # See global_users, will be merged at runtime so you can specify users that are only on 1 host.
```

Dependencies
------------

See defaults/main.yaml for variable defaults that apply to these roles.
[notmycloud.ssh_port_fingerprint](https://github.com/notmycloud/ansible-ssh_port_fingerprint)
[notmycloud.ssh_keyscan](https://github.com/notmycloud/ansible-ssh-keyscan)
[devsec.hardening.ssh_hardening](https://github.com/dev-sec/ansible-collection-hardening/tree/master/roles/ssh_hardening)
[ANXS.tmpreaper](https://github.com/ANXS/tmpreaper)

Example Playbook
----------------

This role doesn't require much configuration as it is opinionated.
You will probably want to set the `global_users` dict at the `group_vars` level and the `host_users` at the `host_vars` level.

```yaml
---
- name: Playbook Name
  hosts: MyHosts
  
  roles:
    - role: notmycloud.linux_defaults
```

License
-------

MIT License

Copyright (c) 2022 Not My Cloud <devops@notmy.cloud>

Permission is hereby granted, free of charge, to any person obtaining a copy  
of this software and associated documentation files (the "Software"), to deal  
in the Software without restriction, including without limitation the rights  
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
copies of the Software, and to permit persons to whom the Software is  
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all  
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR  
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE  
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER  
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,  
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE  
SOFTWARE.

Author Information
------------------

Coming Soon!

Support
------------------

For support, please raise an issue and provide the following items.
Do not reach out directly for support, all requests will be ignored.

- Sample task/playbook to replicate your issue.
- Ansible version `ansible --version`
- Ansible config `ansible-config dump --only-changed -t all`, if using an older version of Ansible, omit the `-t all`.
- Description of what is happening vs what you expect to happen.
