# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provision "shell", inline: <<-SHELL
    PASSWORD="Otus2020"
    ADMIN_GROUP="admin"

    # Create 2 new users user1 and admin1
    useradd -m -s /bin/bash user1 
    useradd -m -s /bin/bash admin1 

    # Set passwords to user1 and admin1
    echo $PASSWORD | passwd --stdin user1
    echo $PASSWORD | passwd --stdin admin1

    # Create ssh dirs and copy auth information 
    mkdir -p ~user1/.ssh
    mkdir -p ~admin1/.ssh
    cp ~vagrant/.ssh/auth* ~user1/.ssh
    cp ~vagrant/.ssh/auth* ~admin1/.ssh

    # Allow to ssh via a password
    sed -i '65s/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
    systemctl restart sshd.service

    # Create admin group and add admin1 and vagrant users to it
    groupadd $ADMIN_GROUP
    gpasswd -a admin1 $ADMIN_GROUP
    gpasswd -a vagrant $ADMIN_GROUP

    # Configure PAM module to allow ssh connections only on workdays for users not in admin group.
    # Users in admin group can connect any day
    cp /vagrant/sshd /etc/pam.d/
    printf 'sshd;*;!root;Wk0000-2400' >> /etc/security/time.conf

  SHELL
end

