# Ansible role for acme.sh

Use this role to get a LetsEncrypt (Le) certificate on your system. The role assumes it's run as root for now.

## Role Variables

Put the ones you need in your groups_vars/host_vars or wherever you set vars:
```yml
# defaults to the host
acme_domain_name: "{{ ansible_host }}"

# webroot or standalone for now
acme_mode: 'webroot'

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

Then run it: `ansible_playbook playbooks/acme.sh.yml` and behold your new cert!

## Notes

### Webroot mode
The parameter "acme_webroot_path" is the web root folder where you host your website files. Acme.sh MUST have write access to this folder, and your webserver needs to be able to read from it (duh!).

### Standalone mode
Requires port 80 to be available, acme.sh will take over the port to listen for the Le callback. You could potentially use the "pre-hook" for this

## TODO

- [ ] test mode for Vagrant
- [ ] Support more modes

## License

MIT

## Author

Based on work by
Fredrik Lundhag, <f@mekk.com>, with changes from <f.lundhag@eyeo.com>
