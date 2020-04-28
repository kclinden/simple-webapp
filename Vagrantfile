Vagrant.configure("2") do |config|
    N = 1
    config.ssh.insert_key = true
    config.ssh.username = "root"
    config.ssh.password = "Passw0rd"
    (1..N).each do |machine_id|
        #Create Container off loop    
        config.vm.define "u#{machine_id}" do |machine|
            machine.vm.hostname = "u#{machine_id}"
            config.vm.provider "docker" do |d|
                d.image = "messiah62/ubuntu-ssh-enabled"
                d.remains_running = true
                d.has_ssh = true
            end
            if machine_id == N
                machine.vm.provision :ansible do |ansible|
                    ansible.limit = "all"
                    ansible.playbook = "./provisioning/playbook.yml"
                end
            end
        end
    end    
  end