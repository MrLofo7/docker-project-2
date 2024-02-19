Vagrant.configure("2") do |config|
    servers=[
        {
          :hostname => "control",
          :box => "centos/7",
          :ip => "169.254.16.48",
          :ssh_port => '2200'
        },
        {
          :hostname => "node1",
          :box => "centos/7",
          :ip => "169.254.16.49",
          :ssh_port => '2201'
        },
        {
          :hostname => "node2",
          :box => "centos/7",
          :ip => "169.254.16.50",
          :ssh_port => '2202'
        }
      ]

    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network :private_network, ip: machine[:ip]
            node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
            node.vm.provider :virtualbox do |vb|
                vb.customize ["modifyvm", :id, "--memory", 512]
                vb.customize ["modifyvm", :id, "--cpus", 1]
            end
        end
    end
end