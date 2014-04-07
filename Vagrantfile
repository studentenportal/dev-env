# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
echo "Installing Python..."
apt-get install -y -qq python
echo "Done."
SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "puppetlabs/debian-7.4-32-nocm"

  # Port forwarding
  config.vm.network :forwarded_port, guest: 8000, host: 8000

  # Do shell provisioning
  config.vm.provision "shell", inline: $script

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision.yml"
    ansible.extra_vars = {
      user_name: "studentenportal",
      project_domain: "studentenportal.ch",
      project_db: "studentenportal"
    }
    ansible.verbose = "vvv"
  end

  # Synchronize the local repo with the server
  config.vm.synced_folder "../web", "/srv/www/studentenportal/", create: true
end
