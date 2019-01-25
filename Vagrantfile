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

Vagrant.configure("2") do |config|
  config.ssh.pty
  if ENV['DISABLE_GLOBAL_PROVISIONER']
    mydebug "Global Provisioner Disabled"
  else
    mydebug "Global Provisioner Enabled"
    config.vm.provision "ansible" do |ansible|
      # has to be full path
      ansible.playbook = "/home/dcarter/.vagrant.d/ansible/playbook.yml"
    end
  end  
end

