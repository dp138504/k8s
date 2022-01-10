# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
#
# For a complete reference of options, please see the online documentation at
# https://docs.vagrantup.com.

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  # VirtualBox Provider options
   config.vm.provider "virtualbox" do |vb|
      # Customize the amount of memory on the VM:
      vb.memory = "512" 

      # Add USB passthru support for YubiKey NFC 5
      vb.customize ["modifyvm", :id, "--usb", "on"]
      vb.customize ["usbfilter", "add", "0", 
        "--target", :id, 
        "--name", "Yubico YubiKey OTP+FIDO+CCID [0524]",
        "--manufacturer", "Yubico",
        "--product", "YubiKey OTP+FIDO+CCID"]
   end

   # Provisioning section.
   config.vm.provision "shell", inline: <<-SHELL
     # Install/configure prefered shell (zsh)
     echo "*** Install/configure prefered shell (zsh) ***"
     apt-get -qqq update > /dev/null 2>&1 && apt-get -qqq install -y zsh > /dev/null 2>&1
     chsh -s /bin/zsh root
     chsh -s /bin/zsh vagrant
     sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" > /dev/null 2>&1
     su - vagrant -c 'sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"' > /dev/null 2>&1
     sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="half-life"/g' /root/.zshrc
     sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="half-life"/g' /home/vagrant/.zshrc

     # Install kubectl
     echo "*** Install kubectl ***"
     apt-get -qqq install -y apt-transport-https ca-certificates > /dev/null 2>&1
     curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
     echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
     apt-get -qqq update > /dev/null 2>&1 && apt-get -qqq install -y kubectl > /dev/null 2>&1

     # Install vsphere kubectl plugin
     echo "*** Install vsphere kubectl plugin ***"
     apt-get -qqq update > /dev/null 2>&1 && apt-get -qqq install -y unzip > /dev/null 2>&1
     wget -q -O /tmp/kubectl-plugins.zip https://172.16.4.13/wcp/plugin/linux-amd64/vsphere-plugin.zip --no-check-certificate
     unzip -qq /tmp/kubectl-plugins.zip -d /usr/local/

     # Update system
     echo "*** Update System ***"
     apt-get -qqq update > /dev/null 2>&1 && apt -qqq upgrade -y > /dev/null 2>&1
     apt -qqq update > /dev/null 2>&1 && apt -qqq upgrade -y > /dev/null 2>&1

     # Setup SSH config file for GitHub push
     echo "*** Setup SSH config file for GitHub push ***"
     cp /vagrant/ssh_config /root/.ssh/config
     echo "DONE: Don't forget to run 'git config --global user.email "you@example.com"'"
     echo "DONE: Don't forget to run 'git config --global user.name "Your Name"'"
     echo "DONE: Make sure to insert your YubiKey and run 'sudo -iH; cd ~/.ssh; ssh-keygen -K'"
   SHELL
end
