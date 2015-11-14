
Vagrant.configure(2) do |config|
  config.vm.hostname = "ipython-vm"

  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 8888, host: 9999

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder "./shared", "/home/vagrant/shared"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096" # Customize the amount of memory on the VM:
  end

  config.vm.provision "shell", inline: <<-SHELL
    echo ">>> UPDATING..."
    sudo apt-get -y update

    echo ">>> INSTALLING PYTHON3 PACKAGE MANAGER..."
    sudo apt-get install -y python3-pip

    echo ">>> INSTALLING JUPYTER..."
    sudo pip3 install jupyter

    # echo ">>> INSTALLING IPYTHON DEPENDENCIES..."

    echo ">>> INSTALLING PYTHON UTILS..."
    sudo apt-get install -y python3-matplotlib
    sudo pip3 install networkx
    sudo pip3 install pykka
    sudo pip3 install pystache

    echo ">>> CLEANING REPOSITORY..."
    sudo apt-get -y autoremove
  SHELL

  config.vm.provision "shell", run: "always", inline: <<-SHELL
     echo "--------------------------------------------------------------------------------------------------"
     echo " Running Jupyter:"
     echo "  * start the jupyter server by accressing the VM with SSH (port:2222, user: vagrant, pw: vagrant)"
     echo "    and run: jupyter notebook /home/vagrant/shared --ip 0.0.0.0 --no-browser"
     echo "  * start working by browsing to http://localhost:9999"
     echo "  * to shut down ipython, press ctrl-C twice in your console that runs vagrant"
     echo "--------------------------------------------------------------------------------------------------"
  SHELL

  # config.vm.post_up_message = "...VM HAS STARTED!"
end
