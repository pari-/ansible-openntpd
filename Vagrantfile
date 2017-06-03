require 'pathname'

HN = Pathname.new(Dir.pwd).basename.to_s.gsub('_','-');

VAGRANTFILE_API_VERSION = "2"

VM_MEM = 1024
VM_CPUS = 1
VM_COUNT = 1
VM_NAME = "vm"
VM_GROUP_NAME = "vm"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  (1..VM_COUNT).each do |i|
    config.vm.define "#{VM_NAME}#{i}" do |subconfig|
      subconfig.vm.box = ENV['VAGRANT_CONFIG_VM_BOX'] || 'parallels/debian-8.8'
      subconfig.vm.hostname = (i == 1) ? HN : HN + i.to_s

      subconfig.vm.provider "parallels" do |prl|
        prl.memory = VM_MEM
        prl.cpus = VM_CPUS
      end

      subconfig.vm.provision :ansible do |ansible|
        ansible.playbook = "test.yml"
        ansible.sudo = true
#	ansible.tags = 'configure'
#       ansible.groups = {
#         "#{VM_NAME}" => "[#{VM_GROUP_NAME}]"
#       }
      end
    end
  end
end
