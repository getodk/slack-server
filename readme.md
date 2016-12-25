## Overview
The `seattle` server runs [http://slack.opendatakit.org](http://slack.opendatakit.org). This repo describes how to setup that machine.

## 1. Provision a remote machine
We currently use a small (512MB, 20GB) box running Ubuntu 16.04.1 LTS on Digital Ocean. We connect via SSH on port 22 with a private key. Passwords are disabled for remote root login.

To ensure Ansible's `ubuntu` user can run passwordless sudo, run `sudo visudo` and confirm these lines below are present, in this order, and are not commented out.

```
root ALL=(ALL:ALL) ALL
admin ALL=(ALL) ALL
ubuntu ALL=(ALL) NOPASSWD: ALL
````

## 2. Install software on your local machine
1. Install [ansible](https://docs.ansible.com/ansible/intro_installation.html) v2.2.0 or later.

## 3. Run ansible to configure remote machine
1. Clone or download this repo.
1. Read over `playbook.yml` and `roles/*/main.yml` to understand behavior.
1. Ensure the correct IP to the machine is in `hosts` file.
1. Ensure `ubuntu.pem`, `slackin.token` and `welcomebot.token` are in `secrets`.
1. Run `ansible-playbook -i hosts playbook.yml`.

## Notes
You may wish to configure ansible to [disable host checking](https://docs.ansible.com/ansible/intro_getting_started.html#host-key-checking) and [disable retry files](https://docs.ansible.com/ansible/intro_configuration.html#retry-files-enabled).
