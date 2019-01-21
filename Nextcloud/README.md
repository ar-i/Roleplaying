# Nextcloud

This playbook installs and configures `Nextcloud` on a machine running a
Debian-based Linux-distribution (tested with Debian Stretch, should work with
Ubuntu as well), using MariaDB as underlying database. Support for Sqlite or
Postgres may or may not be added in the future.

It consists of three different roles:

* `nginx` (installs all software-prerequisites, generates and validates TLS-certificates, downloads Nextcloud)
* `nextcloud-config` (does the actual setup of Nextcloud)
* `smtp` (sets up a basic, send-only mailserver for notifications, password-resets and so on)

The first two are mandatory roles, leaving one of those out will leave you with
a non-functional setup. If you don't feel like you need a mailserver, because
you just use a freemailer or don't give a shit anyway, `smtp` can be left out.


## Prerequisites
You need an A- / AAAA-record pointing towards the IP-address of the machine.
Otherwise this will fail.

On the machine itself, other than you having access with your regular user through SSH and
administrative privileges via `su`, there are no prerequisites. Ansible will
bootstrap all the necessary dependencies by itself.

## Variables
The following variables are necessary to run the playbook. For the role `nginx` (to be defined in
`roles/nginx/vars/main.yml`):

* `hostname` (the hostname of your system, needs to be a FQDN)
* `upload_size` (the maximal filesize per upload, needs to be in the format of `512M`)
* `db_name` (the name for your database)
* `db_username` (the username for the database)
* `db_password` (the password for the database)
* `db_root_password (the root password for MariaDB)

For the role `nextcloud-setup` (to be defined in `roles/nextcloud-setup/vars/main.yml`):

* `hostname` (the hostname of your system, needs to be a FQDN)
* `db_name` (the name for your database)
* `db_username` (the username for the database)
* `db_password` (the password for the database)
* `nextcloud_username` (your login for Nextcloud)
* `nextcloud_password` (your password for Nextcloud)

For the role `smtp` (to be defined in `roles/smtp/vars/main.yml`):

* `hostname` (the hostname of your system, needs to be a FQDN)

## Running
Create a hosts-file, e.g. `hosts.txt` with your targeted host (or hosts, but
that's pointless for this role) in it:

    [all]
    127.0.0.1

Then just execute `ansible-playbook -i hosts.txt -kK  site.yml` - enter your
password, wait a minute and you are done!
