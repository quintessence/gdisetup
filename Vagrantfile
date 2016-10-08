$setup = <<EOF
apt-get -y update
apt-get -y install unzip
apt-get -y install tree
apt-get -y install mysql-client
apt-get -y install postgresql-client
curl -LSs -o /usr/local/bin/jq https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64
chmod 0755 /usr/local/bin/jq

docker pull mysql
docker pull postgres
docker pull quintessence/chinook-mysql

for user in student{1..10} instructor; do
  useradd -m -s /bin/bash -G docker ${user}
done
EOF

Vagrant.configure('2') do |config|
  config.vm.define "gdiclass" do |config|
      config.vm.provision "shell", privileged: false, inline: $setup
      config.vm.provider :digital_ocean do |provider, override|
        override.ssh.private_key_path = '~/.ssh/digitalocean_vagrant'
        provider.ssh_key_name = 'Vagrant'
        override.vm.box = 'digital_ocean'
        override.vm.box_url = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"
        provider.token = ENV['OCEANTOKEN']
        provider.image = 'docker-16-04'           # Docker v1.12.1, Ubuntu 16.04
        provider.region = 'nyc2'
        provider.size = '4gb'
      end
  end
end
