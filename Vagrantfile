servers=[
  {
    :hostname => "manager",
    :ip => "192.168.50.10",
    :box => "ubuntu/xenial64",
    :ram => 1024,
    :cpu => 2
  },
  {
    :hostname => "worker-1",
    :ip => "192.168.50.11",
    :box => "ubuntu/xenial64",
    :ram => 1024,
    :cpu => 2
  },
  {
    :hostname => "worker-2",
    :ip => "192.168.50.12",
    :box => "ubuntu/xenial64",
    :ram => 1024,
    :cpu => 2
  }
]
Vagrant.configure(2) do |config|
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      node.vm.network "private_network", ip: machine[:ip]
      node.vm.provision "docker"
      if machine[:hostname] == "manager"
        node.vm.provision "shell", inline: <<-SHELL
          apt-get update
          apt-get install -y python-pip
          pip install docker-compose
        SHELL
      end
      node.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
      end
    end
  end
end
