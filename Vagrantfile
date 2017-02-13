require 'pathname'

hn = Pathname.new(Dir.pwd).basename.to_s;


VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "parallels/debian-8.6"
  config.vm.hostname = hn

  config.vm.provision :ansible do |ansible|
       ansible.playbook = "test.yml"
       ansible.sudo = true
  end
end
