# Authoritative DNS

This playbook installs and configures `nsd` on a machine running a Debian-based
Linux-distribution (tested with Debian Stretch, should work with Ubuntu as
well), providing a very simple authoritative nameserver for your domain/s.

Please note that this isn't production-ready, you need a second nameserver (or a
third one, if you wanted to have a setup with a hidden master) and you should
probably do more than just run that role and call it a day - look at it as
option to test things quickly.

## Prerequisites
Other than you having access with your regular user through SSH and
administrative privileges via `su`, there are no prerequisites. Ansible will
bootstrap all the necessary dependencies by itself.

## Variables
The following variables are necessary to run the playbook (to be defined in
`roles/nsd/vars/main.yml`):

* `zonelist` (a list of zones you want to manage, the default is `example.com`)

## Running
Create a hosts-file, e.g. `hosts.txt` with your targeted host (or hosts, but
that's pointless for this role) in it:

    [all]
    127.0.0.1

Then just execute `ansible-playbook -i hosts.txt -kK  site.yml` - enter your
password, wait a minute and you are done!
