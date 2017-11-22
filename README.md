## Overview
The `slack` server runs [http://slack.opendatakit.org](http://slack.opendatakit.org). This repo describes how to setup that machine.

## 1. Provision a remote machine
We currently use a small (512MB, 20GB) box running Ubuntu 16.04 LTS on Digital Ocean. We connect via SSH on port 22 with a private key. Passwords are disabled for remote root login.

You will need to [create a user](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart) called `ubuntu` for Ansible to use. To ensure the `ubuntu` user can run passwordless sudo, run `sudo visudo` and confirm these lines below are present, in this order, and are not commented out on the remote machine.

```
# User privilege specification
root    ALL=(ALL:ALL) ALL
ubuntu  ALL=(ALL) NOPASSWD: ALL

# Members of the admin group may gain root privileges
admin   ALL=(ALL) ALL
```

You'll also need to setup [create a RSA key pair](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2) on the remote machine. Once you do:

1. Copy the `~/.ssh/id_rsa` file to `slack-server/secrets/id_rsa` on the local machine. 
1. Add `id_rsa.pub` to `~/.ssh/authorized_keys` on the remote machine.

## 2. Install software on your local machine
1. Install [ansible](https://docs.ansible.com/ansible/intro_installation.html) v2.2.0 or later.

## 3. Run ansible to configure remote machine
1. Clone or download this repo.
1. Read over `playbook.yml` and the files in `roles/` to understand behavior.
1. Ensure the correct IP to the machine is in `hosts` file.
1. Ensure `id_rsa`, `slackin.token` and `welcomebot.token` are in `secrets/`.
1. In `slack-server/`, run `ansible-playbook -i provisioning/hosts provisioning/playbook.yml`.

## Notes
You may wish to configure ansible to [disable host checking](https://docs.ansible.com/ansible/intro_getting_started.html#host-key-checking) and [disable retry files](https://docs.ansible.com/ansible/intro_configuration.html#retry-files-enabled).
