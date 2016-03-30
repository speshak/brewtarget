# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/wily64"
    ubuntu.ssh.forward_x11 = true

    ubuntu.vm.provision "ansible" do |ansible|
      ansible.playbook = "vagrant/ubuntu.yml"
    end
  end

  config.vm.define "freebsd" do |freebsd|
    freebsd.vm.guest = :freebsd
    freebsd.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
    freebsd.vm.box = "freebsd/FreeBSD-11.0-CURRENT"
    freebsd.ssh.shell = "sh"
    freebsd.vm.base_mac = "080027D14C66"
    freebsd.ssh.forward_x11 = true

    freebsd.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
      vb.customize ["modifyvm", :id, "--hwvirtex", "on"]
      vb.customize ["modifyvm", :id, "--audio", "none"]
      vb.customize ["modifyvm", :id, "--nictype1", "virtio"]
      vb.customize ["modifyvm", :id, "--nictype2", "virtio"]
    end

    freebsd.vm.provision "ansible" do |ansible|
      ansible.playbook = "vagrant/freebsd.yml"
    end
  end


end
