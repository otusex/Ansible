MACHINES = {
 :otusc7 => {
    :box_name => "centos/7",
    :ip_addr  => '10.10.0.2',
    :disks    => {
               :sata1 => {
                 :dfile => './sata1.vdi',
                 :size  => '250', #Mb
                 :port  => 1 
                }
    }
  },
}


Vagrant.configure("2") do |config|

 MACHINES.each do |boxname, boxconfig|
   config.vm.synced_folder ".", "/vagrant", disabled: true
   config.vm.define boxname do |box|

      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxname.to_s

      #box.vm.network "forwarded_port", guest: 3260, host: 3260+offset

      box.vm.network "private_network", ip: boxconfig[:ip_addr]

      box.vm.provider :virtualbox do |vb|

           vb.customize ["modifyvm", :id, "--memory", "1024"]
           needsController = false

           boxconfig[:disks].each do |dname, dconf|
             unless File.exist?(dconf[:dfile])
                    vb.customize ['createhd', '--filename', dconf[:dfile], '--variant', 'Fixed', '--size', dconf[:size] ]
                    needsController = true
             end
           end
           if needsController == true
              vb.customize ["storagectl", :id, "--name", "SATA", "--add", "sata"]
              boxconfig[:disks].each do |dname, dconf|
                vb.customize ['storageattach', :id,  '--storagectl', 'SATA', '--port', dconf[:port], '--device', 0, '--type', 'hdd', '--medium', dconf[:dfile]]
              end
           end 
      end
   

   config.vm.provision "ansible" do |ansible|
        ansible.playbook = "play.yml"
        ansible.verbose = "vv"
   end

    end
  end
end


