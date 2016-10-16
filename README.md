# gdisetup
Setup DigitalOcean droplets for GDI Classes

## Requirements

* [Vagrant](https://www.vagrantup.com/docs/why-vagrant/) v 1.7+
* The [DigitalOcean Vagrant plugin](https://www.digitalocean.com/community/tutorials/how-to-use-digitalocean-as-your-provider-in-vagrant-on-an-ubuntu-12-10-vps), to install:<br />`vagrant plugin install vagrant-digitalocean`
* [Packer](https://www.packer.io/intro/) v 0.10.1
* `OCEANTOKEN` environment variable storing your DigitalOcean token
  * [How to generate a DigitalOcean token](https://www.digitalocean.com/community/tutorials/how-to-use-the-digitalocean-api-v2) - note that the token must have Read+Write access

## Cheat Sheet

To change the image and/or size, check what images and sizes are available in your account by:

```
$ vagrant digitalocean-list images ${OCEANTOKEN}
$ vagrant digitalocean-list sizes ${OCEANTOKEN}
```

For more information about the digital_ocean Vagrant plugin, please refer to their [README](https://github.com/devopsgroup-io/vagrant-digitalocean).

## Building/Destroying the DigitalOcean Droplet

To start a DigitalOcean droplet, you will need to clone this repository and save your DigitalOcean token in `tokens/digitaloceantoken` as `OCEANTOKEN`. ([Here](https://www.digitalocean.com/community/tutorials/how-to-use-the-digitalocean-api-v2) is DigitalOcean's documentation explaining how to create the token.)

```
$ source tokens/digitaloceantoken
$ vagrant up
```

When you are done, remember to run `vagrant destroy` from within the project repository to tear down the environment. DigitalOcean charges for spinning up droplets and although the per-hour cost is very low, you might incur unexpected expenses if you forget to destroy your droplet(s).

## Admin Duties

If you wish students to be able to `ssh` into the student envrionment using a password instead of an SSH key, remember to enable `PasswordAuthentication` in `/etc/ssh/sshd_config`.

To setup the student accounts where each student has mysql, postgresql, and chinook-mysql Docker containers, run the `scripts/setup` script on the student environment droplet. Pass the desired default password (for all student accounts) as a parameter:

```
$ curl -o /root/setup \
  https://raw.githubusercontent.com/quintessence/gdisetup/master/scripts/setup
$ chmod 0755 setup
$ ./setup ${default-password}
```

If unspecified, the default password will be `p@ssw0rd`.

If you are a student setting up this environment for yourself, then I'd recommend editing the script to only create a `student` account rather than all 10 student accounts and an instructor account to save time.

## Accessing the containers

By default,`scripts/setup` will create 10 student accounts and an instructor account as well as mysql, postgresql, and chinook-mysql Docker containers for each user. The containers are named by appending the account username to the Docker container type, e.g. `chinook-mysql-student1`. To access a specific Docker container, run the following:

```
$ docker exec -it ${container_name} /bin/bash
```

To view all the containers for your user, run:

```
$ docker ps | grep $(whoami)
```
