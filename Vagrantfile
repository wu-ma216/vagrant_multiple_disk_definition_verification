# -*- mode: ruby -*-
# vi: set ft=ruby :

# Specify the path of additional disk
ADDITIONAL_DISK_PATH = "./.vagrant/disk.vmdk"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  config.disksize.size = '50GB'

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true

  config.vm.synced_folder ".", "/vagrant", type:"virtualbox" ,mount_options: ['uid=0','gid=0','dmode=755','fmode=644']

  config.vm.define "myoko" do |server|
    server.vm.hostname = "myoko.test"

    server.vm.network "private_network", ip: "192.168.0.50"

    # Omit guest additions updates in terms of trying `vagrant up` repeatedly
    server.vbguest.auto_update = false
    # accelerattion for apt package installations
    #server.vbguest.installer_hooks[:before_install] = ['sed -i-`date +%Y%m%d` -r "s%http://(jp.)?archive.ubuntu.com/ubuntu%https://linux.yz.yamagata-u.ac.jp/ubuntu%" /etc/apt/sources.list',
    #                                                    'apt update' ]

    # cleanup additional disk after "destroy" action
    config.trigger.after :destroy do |trigger|
      trigger.name = "Cleanup additional disk operation started"
      # Ruby code to be executed on the host
      trigger.ruby do
        if File.exist?(ADDITIONAL_DISK_PATH)
          system("vboxmanage closemedium disk '#{ADDITIONAL_DISK_PATH}' --delete")
        end

        puts "Cleanup additional disk operation Ended successfully"
      end
    end

    server.vm.provider "virtualbox" do |vb|
      vb.cpus = 1
      vb.memory = 1024
      vb.name = "myoko.test"
      unless File.exist?(ADDITIONAL_DISK_PATH)
         vb.customize [ "createmedium", "disk", "--filename", ADDITIONAL_DISK_PATH, "--format", "vmdk", "--size", 40 * 1024 ]
      end
      # Specify SCSI port 2 because SCSI port 1 has already been used at Ubuntu Focal Fossa box file.
      vb.customize [ "storageattach", vb.name, "--storagectl", "SCSI", "--port", "2", "--device", "0", "--type", "hdd", "--medium", ADDITIONAL_DISK_PATH ]
    end
  end
end
