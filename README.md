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

## Admin Duties

If you wish students to be able to `ssh` into the student envrionment using a password instead of an SSH key, remember to enable `PasswordAuthentication` in `/etc/ssh/sshd_config`.

To setup the student accounts where each student has mysql, postgresql, and chinook-mysql Docker containers, run the `scripts/setup` script on the student environment droplet. Pass the desired default password (for all student accounts) as a parameter:

```
./scripts/setup ${default-password}
```

If unspecified, the default password will be `p@ssw0rd`.

## Accessing the containers

By default, the `Vagrantfile` and `scripts/setup` will setup 10 student accounts, named `student1` ... `student10` and will append the account username to the Docker container type, e.g. `chinook-mysql-student1`, to separate which containers are for which users. Use the following command to list the container IDs and names with the containers associated (by name only) with the account you are logged in as:

```
docker ps | grep $(whoami) | awk '{print $1 "\t" $NF}'
```

To access a specific Docker container, run the following using the container ID that matches the container you wish to enter:

```
docker exec -it ${container_id} /bin/bash
```

You can also use the container name in place of the container ID.

## Important Potential Issue

Please read [Github Issue #178](https://github.com/devopsgroup-io/vagrant-digitalocean/issues/178) for an issue with SSH keys and Vagrant's DigitalOcean plugin. Although some users report being able to use only the name of the key if it's already been added to DigitalOcean, my experience has been somewhat inconsistent in that sometimes I need to remove the key from DigitalOcean so it is "new" and other times I do not. Your mileage may vary.
