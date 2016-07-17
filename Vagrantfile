# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  if Vagrant.has_plugin?("vagrant-vbguest") then
    # Guest Additions自動更新の無効化設定
    #config.vbguest.auto_update = false
  end

  if Vagrant.has_plugin?("vagrant-cachier") then
    config.cache.scope = :box
  end

  config.vm.box = "bento/centos-6.7"
  config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", mount_options: ["dmode=777", "fmode=666"]

  # 1台目の設定 (webサーバー)
  config.vm.define "web1" do |server|
    server.vm.hostname = "web1"
    server.vm.network "private_network", ip: "192.168.33.10"

    # VirtualBoxのGUI上の名前 (デフォルトだと長い名前になるので)
    server.vm.provider "virtualbox" do |vb|
      vb.name = config.vm.box.gsub(/\//, "-") + "-" + server.vm.hostname
    end

    # vagrant destroy実行時に"playbookが無い"と言われてしまうので
    # vagrant up, vagrant provision実行時のみ通るようにする
    if ARGV[0] == "up" || ARGV[0] == "provision" then
      server.vm.provision "ansible_local" do |ansible|
        ansible.inventory_path = "./playbook/hosts/local"
        ansible.playbook       = "./playbook/webservers.yml"
        ansible.limit          = "webservers"
      end
    end
  end

=begin
  # 2台目の設定 (dbサーバー)
  config.vm.define "db1" do |server|
    server.vm.hostname = "db1"
    server.vm.network "private_network", ip: "192.168.33.20"

    server.vm.provider "virtualbox" do |vb|
      vb.name = config.vm.box.gsub(/\//, "-") + "-" + server.vm.hostname
    end

    if ARGV[0] == "up" || ARGV[0] == "provision" then
      server.vm.provision "ansible_local" do |ansible|
        ansible.inventory_path = "./playbook/hosts/local"
        ansible.playbook       = "./playbook/dbservers.yml"
        ansible.limit          = "dbservers"
      end
    end
  end
=end

end
