# Vagrant 1.6.5

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "dev"
    config.vm.network "private_network", ip: "192.168.10.145"
    config.vm.synced_folder "../source", "/var/www/", type: "nfs"
    config.vm.provision "ansible" do |ansible|
        ansible.limit = 'all'
        ansible.sudo = true
        ansible.sudo_user = "root"
        ansible.verbose = 'v'
        ansible.playbook = "../ansible/vagrant.yml"
        ansible.inventory_path = "../ansible/local"
        ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    end
end
