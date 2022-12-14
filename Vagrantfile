# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 256]
  end

  config.vm.define :haproxy, primary: true do |haproxy_config|

    haproxy_config.vm.hostname = 'haproxy'
    haproxy_config.vm.network :forwarded_port, guest: 8080, host: 8080
    haproxy_config.vm.network :forwarded_port, guest: 80, host: 8081

    haproxy_config.vm.network :private_network, ip: "192.168.56.10"
    haproxy_config.vm.provision "file", source: "files/haproxy", destination: "$HOME/files"
    haproxy_config.vm.provision :shell, :path => "scripts/common.sh"
    haproxy_config.vm.provision :shell, :path => "scripts/haproxy-setup.sh"


  end
  config.vm.define :web1 do |web1_config|

    web1_config.vm.hostname = 'web1'
    web1_config.vm.network :private_network, ip: "192.168.56.11"
    web1_config.vm.provision :shell, :path => "scripts/common.sh"
    web1_config.vm.provision :shell, :path => "scripts/web-setup.sh"


  end
  config.vm.define :web2 do |web2_config|

    web2_config.vm.hostname = 'web2'
    web2_config.vm.network :private_network, ip: "192.168.56.12"
    web2_config.vm.provision :shell, :path => "scripts/common.sh"
    web2_config.vm.provision :shell, :path => "scripts/web-setup.sh"

  end
  config.vm.define :cdn do |cdn_config|

    cdn_config.vm.hostname = 'cdn'
    cdn_config.vm.network :private_network, ip: "192.168.56.13"
    cdn_config.vm.provision "file", source: "files/cdn", destination: "$HOME/files"
    cdn_config.vm.provision :shell, :path => "scripts/common.sh"
    cdn_config.vm.provision :shell, :path => "scripts/cdn-setup.sh"

  end
end