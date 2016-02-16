# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
$script = <<SCRIPT
# limits
ulimit -n 10000
echo "" > /etc/hosts
echo "127.0.0.1 $1 $1.localdomain" >> /etc/hosts
echo "::1 $1 $1.localdomain" >> /etc/hosts
echo "192.168.2.51 node1 node1.localdomain" >> /etc/hosts
echo "192.168.2.52 node2 node2.localdomain" >> /etc/hosts
echo "192.168.2.53 node3 node3.localdomain" >> /etc/hosts
echo "192.168.2.54 node4 node4.localdomain" >> /etc/hosts
echo "192.168.2.55 node5 node5.localdomain" >> /etc/hosts
echo "192.168.2.56 kdc kdc.localdomain" >> /etc/hosts
echo "192.168.2.57 web web.localdomain" >> /etc/hosts
SCRIPT

Vagrant.configure(2) do |config|

  config.vm.synced_folder ".", "/vagrant", :disabled => true
  config.vm.box_url = "hdp_base"
  config.ssh.username = "root"
  config.ssh.password = "root"


  config.vm.define "hdp_dn1" do |hdp_dn1|
    hdp_dn1.vm.box = "hdp"
    hdp_dn1.vm.hostname = "node3"
    hdp_dn1.vm.network "public_network", ip: "192.168.2.53", netmask: "255.255.255.0", hostsupdater: "skip"
    hdp_dn1.vm.provision "shell", inline: $script, args: "node3"
  end

  config.vm.define "hdp_dn2" do |hdp_dn2|
   hdp_dn2.vm.box = "hdp"
   hdp_dn2.vm.hostname = "node4"
   hdp_dn2.vm.network "public_network", ip: "192.168.2.54", netmask: "255.255.255.0", hostsupdater: "skip"
   hdp_dn2.vm.provision "shell", inline: $script, args: "node4"
  end
end
