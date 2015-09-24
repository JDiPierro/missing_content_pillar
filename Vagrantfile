VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  machine_name = "salt-empty-pillar"
  config.vm.define machine_name do |machine|
    machine.vm.box = "ubuntu/trusty64"
    machine.vm.host_name = machine_name
    machine.vm.network "public_network", :bridge => "en0: Wi-Fi (AirPort)"

    machine.vm.synced_folder "./states", "/srv/salt"
    machine.vm.synced_folder "./pillar", "/srv/pillar"

    machine.vm.provision :salt do |salt|
      salt.install_type = :git
      salt.install_args = "v2015.8.0"
      salt.bootstrap_options = '-P -Z'
      salt.run_highstate = true

      salt.log_level = "info"
      salt.colorize = true
      salt.verbose = true

      salt.minion_config = "./minion"
    end
  end
end