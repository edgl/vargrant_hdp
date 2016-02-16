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
  config.ssh.username = "root"
  config.ssh.password = "root"

	config.vm.define "web" do |web|
		web.vm.provider "virtualbox" do |v|
			v.memory = 512
		end
		web.vm.provision "shell", inline: "yum install apache"
    web.vm.box = "hdp"
    web.vm.hostname = "web"
    web.vm.network "public_network", ip: "192.168.2.57", netmask: "255.255.255.0", hostsupdater: "skip"
    web.vm.provision "shell", inline: $script, args: "web"
	end

  config.vm.define "hdp_ambari" do |hdp_ambari|
    hdp_ambari.vm.box = "hdp"
    hdp_ambari.vm.hostname = "node5"
    hdp_ambari.vm.network "public_network", ip: "192.168.2.55", netmask: "255.255.255.0", hostsupdater: "skip"
    hdp_ambari.vm.provision "shell", inline: $script, args: "node5"
  end

  config.vm.define "hdp_nn" do |hdp_nn|
    hdp_nn.vm.box = "hdp"
    hdp_nn.vm.hostname = "node1"
    hdp_nn.vm.network "public_network", ip: "192.168.2.51", netmask: "255.255.255.0", hostsupdater: "skip"
    hdp_nn.vm.provision "shell", inline: $script, args: "node1"
  end

  config.vm.define "hdp_snn" do |hdp_snn|
   hdp_snn.vm.box = "hdp"
   hdp_snn.vm.hostname = "node2"
   hdp_snn.vm.network "public_network", ip: "192.168.2.52", netmask: "255.255.255.0", hostsupdater: "skip"
   hdp_snn.vm.provision "shell", inline: $script, args: "node2"
  end
end
