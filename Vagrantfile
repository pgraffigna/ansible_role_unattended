ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
IMAGEN = "generic/ubuntu2004"

$script = <<-SCRIPT
  sudo apt-get update && sudo apt-get install unattended-upgrades -y
SCRIPT

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", type: "rsync", disabled: true

  config.vm.define :server do |s|
    s.vm.box = IMAGEN
    s.vm.hostname = "ubuntu"
    s.vm.box_check_update = false
    s.vm.provision "shell", inline: $script

    s.vm.provider :libvirt do |v|
      v.memory = 1024
      v.cpus = 2
    end
  end
end

# /etc/apt/apt.conf.d/50unattended-upgrades