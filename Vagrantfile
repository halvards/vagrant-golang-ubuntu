# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|

  # Base box (from Hashicorp Atlas)
  config.vm.box = 'halvards/lubuntu64'

  # Assign this VM a unique hostname
  config.vm.host_name = "#{ENV['USER']}.golang.ubuntu64.vagrantup.com"

  # Copy private key to VM for Git and other tools
  config.vm.provision 'file', source: '~/.ssh/id_rsa', destination: '~/.ssh/id_rsa'

  # Provision VM with Ansible (will not work for Windows hosts)
  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'playbook.yml'
    ansible.verbose = 'vv' # v, vv, vvv, vvvv
    ansible.sudo = true
    ansible.sudo_user = 'root'
  end

  # Forward a port from the guest to the host
  config.vm.network 'forwarded_port', guest: 22,   host: 2191, id: 'ssh', auto_correct: true
  config.vm.network 'forwarded_port', guest: 9000, host: 9000, auto_correct: true # Web server
  config.vm.network 'forwarded_port', guest: 5432, host: 5432, auto_correct: true # PostgreSQL server

  # Share a folder to the VM (host path, guest path)
  config.vm.synced_folder '~/golang', '/home/vagrant/golang'

  config.vm.provider 'virtualbox' do |vb|
    # Boot with a GUI so you can see the screen. (Default is headless)
    vb.gui = true

    # Set name of VirtualBox VM
    vb.name = 'golang-ubuntu64'

    # Set memory allocated to the VM in MB
    vb.customize ['modifyvm', :id, '--memory', '4096']
    vb.customize ['modifyvm', :id, '--cpus', '2']
    vb.customize ['modifyvm', :id, '--vram', '256']
    vb.customize ['modifyvm', :id, '--accelerate2dvideo', 'off']
    vb.customize ['modifyvm', :id, '--accelerate3d', 'on']

    # Enable shared clipboard
    vb.customize ['modifyvm', :id, '--clipboard', 'bidirectional']

    # Suppress some VirtualBox messages
    vb.customize ['setextradata', :id, 'GUI/SuppressMessages', 'remindAboutAutoCapture,remindAboutWrongColorDepth,remindAboutMouseIntegrationOn,remindAboutMouseIntegrationOff,confirmInputCapture,confirmGoingFullscreen']

    # Make DNS work across host VPN connection
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
  end
end

