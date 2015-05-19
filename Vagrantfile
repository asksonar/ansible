Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Ready"

  config.vm.box = "ubuntu/trusty64" # Official Ubuntu Server 14.04 LTS (Trusty Tahr) builds
  config.vm.network "private_network", type: "dhcp"
  config.vm.synced_folder "~/sonar", "/var/src"
  # config.vm.synced_folder "~/log/postgresql", "/var/log/postgresql"
  # config.vm.synced_folder "~/lib/postgresql", "/var/lib/postgresql"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  # resolve ip addresses set via dhcp
  # src: https://github.com/smdahlen/vagrant-hostmanager/issues/86
  config.hostmanager.ip_resolver = proc do |vm, resolving_vm|
    if vm.id
      `VBoxManage guestproperty get #{vm.id} "/VirtualBox/GuestInfo/Net/1/V4/IP"`.split()[1]
    end
  end

  config.vm.define "web" do |web|
    web.vm.hostname = "my.asksonar.local"
  end

  config.vm.define "db" do |db|
    db.vm.hostname = "db.asksonar.local"
  end

  config.vm.define "video" do |video|
    video.vm.hostname = "video.asksonar.local"
  end
end
