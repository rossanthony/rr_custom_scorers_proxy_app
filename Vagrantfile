# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

domain = "rr-custom-app.local"
settings = {
  :hostname => "rr-custom-app",
  :box => "hashicorp/precise64",
  :ip => "192.168.33.10",
}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    # Box name
    config.vm.box = settings[:box]

    # Hostname
    config.vm.host_name = "#{settings[:hostname]}.#{domain}"

    # Provider box url
    config.vm.box = "#{settings[:box]}"

    # Port forwarding
    config.vm.network :forwarded_port, guest: 80, host: 8080

    # Host-only access private network
    config.vm.network :private_network, ip: settings[:ip]

    # Shared folders
    config.vm.synced_folder "/Users/rossanthony/rr_custom_scorers_proxy_app", "/var/www/#{settings[:hostname]}.#{domain}"

    # Puppet config
    config.vm.provision :puppet do |puppet|
        puppet.manifests_path = "vagrant/puppet/manifests"
        puppet.manifest_file  = "site.pp"
        puppet.module_path = "vagrant/puppet/modules"
    end

end