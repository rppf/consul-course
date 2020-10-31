Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provision "shell", path: "provision/install-consul.sh", privileged: false

  config.vm.define "consul-server" do |cs|
    cs.vm.hostname = "consul-server"
    cs.vm.network "private_network", ip: "172.20.20.31"
  end

  config.vm.define "lb" do |lb|
    lb.vm.hostname = "lb"
    lb.vm.network "private_network", ip: "172.20.20.11"
    lb.vm.provision "shell", path: "provision/install.docker.sh", privileged: false
  end

  (1..3).each do |i|
    config.vm.define "web#{i}" do |web|
      web.vm.hostname = "web#{i}"
      web.vm.network "private_network", ip: "172.20.20.2#{i}"
      web.vm.provision "shell", path: "provision/install.docker.sh", privileged: false
    end
  end
end
