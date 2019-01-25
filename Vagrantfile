# -*- mode: ruby -*-
# vi: set ft=ruby :

# debugging method

def mydebug (message)
  if ENV['DEBUG_VAGRANTFILES']
    puts message + "\n\n"
  end
end

mydebug "this is the global vagrantfile in ~/.vagrant.d/"

mydebug "Debugging Vagrant files: ARGV = #{ARGV}"

require 'pp'

Vagrant.configure("2") do |config|
  config.ssh.pty
  if ENV['DISABLE_GLOBAL_PROVISIONER']
    mydebug "Global Provisioner Disabled"
  else
    mydebug "Global Provisioner Enabled"

    mydebug "starting shell provisioner"
    config.vm.provision "shell" do |s|
      s.inline = <<-SHELL
        source /etc/os-release; if [[ ${ID} -eq 'fedora' || ${ID} -eq 'centos' ]]; then yum -y install python-simplejson; fi
      SHELL
    end

    mydebug "starting ansible provisioner"
    config.vm.provision "ansible" do |ansible|
      # has to be full path
      ansible.playbook = "/home/dcarter/.vagrant.d/ansible/playbook.yml"
    end
  end  
end

