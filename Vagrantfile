Vagrant.configure("2") do |config|
  #Config memory and cpu usage
  config.vm.provider "virtualbox" do |v|
    v.memory = 512;
    v.cpus = 1;
  end

  config.vm.box = "ubuntu/xenial64"

  #Manager als load balancer
  config.vm.define "mgr" do |mgr|
    mgr.vm.hostname = "mgr.site"
    mgr.vm.network "private_network", ip: "192.168.50.10"
    mgr.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
    mgr.vm.provision "shell", path: "bootstrap.sh"
  end

  #Database configuratie
  config.vm.define "database" do |db|
    db.vm.hostname = "db.site"
    db.vm.network "private_network", ip: "192.168.50.11"
    db.vm.provision "shell", path: "bootstrap.sh"
  end

  #Cache .12-15
    #For each in I (11+1,11+2,11+3,11+4)
    (1..4).each  do |i|
      config.vm.define "cache#{i}" do |cache|
        cache.vm.hostname = "cache#{i}.site"
        cache.vm.network "private_network", ip: "192.168.50.#{11+i}"
        cache.vm.provision "shell", path: "bootstrap.sh"
      end
    end

  #Frontapp .17-20
    #For each in I (16+1,16+2,16+3,16+4)
    (1..4).each do |i|
      config.vm.define "front#{i}" do |front|
        front.vm.hostname = "front#{i}.site"
        front.vm.network "private_network", ip: "192.168.50.#{16+i}"
        front.vm.provision "shell", path: "bootstrap.sh"
      end
    end
end
