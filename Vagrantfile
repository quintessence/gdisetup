Vagrant.configure('2') do |config|
  config.vm.define "gdiclass" do |config|
      config.vm.provider :digital_ocean do |provider, override|
        override.ssh.private_key_path = '~/.ssh/digitalocean_vagrant'
        provider.ssh_key_name = 'Vagrant'
        override.vm.box = 'digital_ocean'
        override.vm.box_url = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"
        provider.token = ENV['OCEANTOKEN']
        provider.image = 'docker-16-04'           # Docker v1.12.1, Ubuntu 16.04
        provider.region = 'nyc2'
        provider.size = '512mb'
      end
  end
end
