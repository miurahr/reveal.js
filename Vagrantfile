# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "trusty"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-i386-vagrant-disk1.box"

  config.vm.provider :aws do |aws, override|
    aws.access_key_id             = "ACCESS_KEY_ID"
    aws.secret_access_key         = "SECRET_ACCESS_KEY"
    aws.keypair_name              = "KEYPAIR"
    override.ssh.private_key_path = "PRIVATE_KEYPATH"

    ## saucy64
    ## instance-store
    aws.region_config 'ap-northeast-1', :ami => "ami-f75c37f6"
    #aws.region_config "eu-west-1",      :ami => "ami-3cfc0a4b"
    #aws.region_config "us-west-1",      :ami => "ami-c0370a85"
    ## ebs
    #aws.region_config "ap-northeast-1", :ami => "ami-fd5239fc"
    #aws.region_config "us-west-1",      :ami => "ami-96370ad3"

    aws.instance_type     = "m1.small"
    override.vm.box       = "dummy"
    override.ssh.username = "ubuntu"
  end

  config.vm.provider :kvm do |kvm, override|
    kvm.gui = true
    override.vm.box_url = "https://vagrant-kvm-boxes.s3.amazonaws.com/trusty64_kvm.box"
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.auto_detect = true
  end

  config.vm.provision :shell, inline: <<-SH
    set -x
    export DEBIAN_FRONTEND=noninteractive

    apt-get update

    apt-get -y install npm nodejs nodejs-legacy git
    npm install -g grunt-cli
    git clone https://github.com/hakimel/reveal.js.git
    cd reveal.js
    npm install
    #
    echo "You can now login with 'vagrant ssh'"
    echo "and run with 'grunt serve --bind 0.0.0.0 --port 8000'"
  SH

  # config.vm.network :forwarded_port, guest: 8000, host: 8080
  # config.vm.network :private_network, ip: "192.168.33.10"

end
