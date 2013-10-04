# vi: set ft=ruby :

# Cache apt-packages automatically
# Make the PIP download cache easier
Vagrant.require_plugin 'vagrant-cachier'

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'precise64'
  config.vm.box_url = 'http://cloud-images.ubuntu.com/precise/current/' +
                      'precise-server-cloudimg-vagrant-amd64-disk1.box'

  config.vm.network :forwarded_port, guest: 8000, host: 8000
  config.ssh.forward_agent = true

  config.cache.auto_detect = true
  host_pip = File.expand_path("~/.vagrant.d/cache/#{config.vm.box}/pip")
  unless File.directory?(host_pip)
    require 'fileutils'
    FileUtils.mkdir_p host_pip
  end

  config.vm.synced_folder '.', '/home/vagrant/ip-provision'

  config.vm.provision :shell do |shell|
    shell.inline = 'apt-get update && apt-get install --yes python-pip && pip install Django --download-cache /tmp/vagrant-cache/pip'
  end
end
