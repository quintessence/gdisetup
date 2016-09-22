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

## Important note

Please read [Github Issue #178](https://github.com/devopsgroup-io/vagrant-digitalocean/issues/178) for an issue with SSH keys and Vagrant's DigitalOcean plugin. Although some users report being able to use only the name of the key if it's already been added to DigitalOcean, my experience has been that I need to remove the key from DigitalOcean so it is "new" every time. Your mileage may vary.
