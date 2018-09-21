# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "rhel-7.5"

  config.vm.hostname = "node01"

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider :libvirt do |domain|
      domain.memory = 2048
      domain.cpus = 2
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "subscribe.yml"
    ansible.ask_vault_pass = true
  end

  config.vm.trigger.before :destroy do |trigger|
    trigger.warn = "Unsubscribe"
    trigger.run_remote = {inline: "subscription-manager unsubscribe --all && subscription-manager unregister"}
  end
end
