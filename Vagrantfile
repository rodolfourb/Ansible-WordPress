# -*- mode: ruby -*-
# vi: set ft=ruby :

vms = {
	'wordpress'   => {'memory' => '1024', 'cpus' => 2, 'ip' => '007', 'box' => 'almalinux/8', 'provision' => 'files/ansible/playbook.yml'},
	'mysql' => {'memory' => '1024', 'cpus' => 2, 'ip' => '008', 'box' => 'almalinux/8', 'provision' => 'files/ansible/bd-mysql.yml'}
}

Vagrant.configure('2') do |config|
	config.vm.box_check_update = false
	vms.each do |name, conf|
		config.vm.define "#{name}" do |k|
			k.vm.hostname = "#{name}.wordpress.local"
			k.vm.network 'private_network', ip: "192.168.56.#{conf['ip']}"
			k.vm.box = conf['box']
			k.vm.provider 'virtualbox' do |vb|
				vb.memory = conf['memory']
				vb.cpus = conf['cpus']
			end
			k.vm.provision 'ansible_local' do |ansible|
				ansible.playbook = "#{conf['provision']}"
			end
		end
	end

		
end
