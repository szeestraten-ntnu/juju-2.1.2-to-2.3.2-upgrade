Vagrant.configure(2) do |config|
  # Box
  config.vm.box = "bento/ubuntu-16.04"

  # Run playbook
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yaml"
  end

  # VirtualBox settings
  config.vm.provider "virtualbox" do |vbox|
    vbox.memory = 3072
  end
end
