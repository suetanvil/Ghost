# -*- mode: ruby -*-
# vi: set ft=ruby :

#EXTRA_FOLDER=
#  File.exists?("BUILD_DIR") ? IO.readlines("BUILD_DIR")[0].chomp : "";
#EXTRA_MNT = "/vagrant-extra"

CORES=
  File.exists?("NUM_CORES") ? IO.readlines("NUM_CORES")[0].chomp : "1";

INSTALL_SCRIPT=<<EOF
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install -y nodejs npm
EOF

# RB_PATH_SCRIPT=<<EOF
# if [ -f /home/vagrant/.profile ] && grep -q setrubypath.sh /home/vagrant/.profile
# then
#   true
# else
#   echo '. /vagrant/cfg_scripts/setrubypath.sh' >> /home/vagrant/.profile
# fi
# EOF


Vagrant.configure("2") do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise32"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
#  config.vm.box_url = "http://files.vagrantup.com/precise32.box"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/precise/" +
    "current/precise-server-cloudimg-amd64-vagrant-disk1.box"

  # Install packages
  config.vm.provision :shell, :inline => INSTALL_SCRIPT

  # Set the ruby path
#  config.vm.provision :shell, :inline => RB_PATH_SCRIPT

  # The third-party build dir has to be provided via the launch script.
  # if EXTRA_FOLDER.size > 0
  #   config.vm.synced_folder EXTRA_FOLDER, EXTRA_MNT
  # end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--cpus", CORES]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]   # Needed for some AMD processors
  end
end
