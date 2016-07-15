# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :private_network, ip:'10.10.11.21'

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks", "site-cookbooks"]

    chef.add_recipe "apt"
    chef.add_recipe "nodejs"
    chef.add_recipe "ruby_build"
    chef.add_recipe "ruby_rbenv::user"
    chef.add_recipe "vim"
    chef.add_recipe "postgresql::server"

    chef.json = {
      rbenv: {
        user_installs: [{
          user: 'vagrant',
          rubies: ["2.3.1"],
          global: "2.3.1",
          gems: {
            "2.3.1" => [
              { name: "bundler" }
            ]
          }
        }]
      },
      postgresql: {
        password: {
          postgres: ''
        }
      }
    }

  end
end
