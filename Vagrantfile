# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "fscm/cassandra"

  config.vm.network "forwarded_port", guest: 8778, host: 8778

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
    wget 'http://search.maven.org/remotecontent?filepath=org/jolokia/jolokia-jvm/1.3.7/jolokia-jvm-1.3.7-agent.jar' \
      -O /srv/cassandra/lib/jolokia-jvm-1.3.7-agent.jar
    echo '-javaagent:/srv/cassandra/lib/jolokia-jvm-1.3.7-agent.jar=host=*,port=8778,discoveryEnabled=false' \
      >> /srv/cassandra/conf/jvm.options
    service cassandra restart
  SHELL
end
