Vagrant.configure("2") do |config|

    config.vm.define "db" do |u1|
        u1.vm.box = "hashicorp/bionic64"
        u1.vm.hostname = "db"
        u1.vm.network "private_network", ip: "192.168.50.2"
        config.vm.provider "vmware_desktop" do |v|
            v.vmx["numvcpus"] = "1"
            v.vmx["memsize"] = "512"
        end 
    end

    config.vm.define "web" do |u2|
        u2.vm.box = "hashicorp/bionic64"
        u2.vm.hostname = "web"
        u2.vm.network "private_network", ip: "192.168.50.3"
        config.vm.provider "vmware_desktop" do |v|
            v.vmx["numvcpus"] = "1"
            v.vmx["memsize"] = "512"
        end   
    end

    config.vm.provision "ansible" do |ansible|
        ansible.become = true
        ansible.groups = {
            "db" => ["db"],
            "web" => ["web"]
        }
        ansible.playbook = "provisioning/playbook.yml"
    end 

end