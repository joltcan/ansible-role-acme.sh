# Ansible role for acme.sh

Use this role to get a LetsEncrypt (Le) certificate on your system. The role assumes it's run as root for now.

## Role Variables

Put the ones you need in your groups_vars/host_vars or wherever you set vars:
```yml
# defaults to the host
acme_domain_name: "{{ ansible_host }}"

# webroot or standalone for now
<<<<<<< HEAD
acme_mode: 'standalone'
=======
acme_mode: 'webroot'
>>>>>>> b02fc5666ada62b71cc9e3c8516bb2a930e90d0c

# Where to install the cert when it's ready
acme_fullchain_file: /etc/ssl/certs/{{ acme_domain_name }}.pem
acme_key_file: /etc/ssl/private/{{ acme_domain_name }}.key

# What to do when the certs are renewed
acme_reload_cmd: ""

# Maybe you want to do something more here, like systemctl stop nginx
acme_post_hook: ""

# Maybe you want to do something more here, like chown <someuser> {{ acme_key_file }} ; systemctl start nginx
acme_pre_hook: ""

# Where to put the Le response code. 
acme_webroot_path: "/{{ acme_user }}/.acme.sh/webroot/"

```

## Playbook Example

Simple as pie! Save this into a playbook

```yml
---
- hosts: someservers 
  roles:
    - role: role/ansible-role-acme.sh
```

<<<<<<< HEAD
Then run it: `ansible-playbook playbooks/acme.sh.yml` and behold your new cert!
=======
Then run it: `ansible_playbook playbooks/acme.sh.yml` and behold your new cert!
>>>>>>> b02fc5666ada62b71cc9e3c8516bb2a930e90d0c

## Notes

### Webroot mode
The parameter "acme_webroot_path" is the web root folder where you host your website files. Acme.sh MUST have write access to this folder, and your webserver needs to be able to read from it (duh!).

### Standalone mode
<<<<<<< HEAD
Requires port 80 to be available, acme.sh will take over the port to listen for the Le callback.
=======
Requires port 80 to be available, acme.sh will take over the port to listen for the Le callback. You could potentially use the "pre-hook" for this
>>>>>>> b02fc5666ada62b71cc9e3c8516bb2a930e90d0c

## TODO

- [ ] test mode for Vagrant
- [ ] Support more modes

## License

MIT

## Author

<<<<<<< HEAD
Based on work by
Fredrik Lundhag, <f@mekk.com>, with changes from <f.lundhag@eyeo.com>
=======
Fredrik Lundhag, <f@mekk.com>
>>>>>>> b02fc5666ada62b71cc9e3c8516bb2a930e90d0c
