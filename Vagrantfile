# -*- mode: ruby -*-
# vi: set ft=ruby :
# Префикс для LAN сети
BRIDGE_NET="192.168.1."
# Массив из хешей, в котором заданы настройки для каждой виртуальной машины
servers=[
#  {
#    :hostname => "web1.",
#    :ip => BRIDGE_NET + "101",
#    :ram => 256
#  },
#  {
#    :hostname => "web2.",
#    :ip => BRIDGE_NET + "102",
#    :ram => 256
#  },
  {
    :hostname => "hp1.",
    :ip => BRIDGE_NET + "103",
    :ram => "512",
    :hostport => "8000",
    :guestport => "80"

  },
#  {
#    :hostname => "jenkins.",
#    :ram => 512,
#  }
]

# Входим в Главную конфигурацию vagrant версии 2
Vagrant.configure(2) do |config|
    # Добавить шару между хостовой и гостевой машиной
    #config.vm.synced_folder "D://hostmachine/shared/folder", "/src/shara"
    # Отключить дефолтную шару
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.network :forwarded_port, guest: 80, host: 8000
    # Проходим по элементах массива "servers"
    servers.each do |machine|
        # Применяем конфигурации для каждой машины. Имя машины(как ее будет видно в Vbox GUI) находится в переменной "machine[:hostname]"
        config.vm.define machine[:hostname] do |node|
            # Поднять машину из образа "ubuntu 14.04", который мы создали в предыдущей статье
            node.vm.box = "trusty64"
            # Также, можно указать URL откуда стянуть нужный box если такой есть
            #node.vm.box_url = "http://files.vagrantup.com/precise64.box"
            # Пул портов, который будет использоваться для подключения к каждый VM через 127.0.0.1
#            node.vm.usable_port_range = (2200..2250)
            # Hostname который будет присвоен VM (самой ОС)
            node.vm.hostname = machine[:hostname]
            #VBoxManage.exe list bridgedifs overwrite NAT adapter :adapter=>1
            # Добавление и настройка Bridge сетевого адаптера(моста). Чтобы узнать точное название birdge адаптера, нужно использовать VBoxManage.exe (смотрите ниже)
            node.vm.network "public_network", ip: machine[:ip], bridge: 'eth0'

  #          if [:hostname] == "hp1"?
  #            node.vm.network :forwarded_port, guest: 80, host: 8000
  #          fi
            # Настройка SSH доступа
            # Домен/IP для подключения
            #node.ssh.host = machine[:ip]
            # Для доступа по ранее добавленному ключу
            #node.ssh.private_key_path = "private_key"
            # SSH логин пользователя
            #node.ssh.username = "ivan"
            # SSH пароль
            #node.ssh.password = "vagrant"
            # Тонкие настройки для конкретного провайдера (в нашем случаи - VBoxManage)
            node.vm.provider "virtualbox" do |vb|
                # Размер RAM памяти
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
                # Можно перезаписать название VM в Vbox GUI
                vb.name = machine[:hostname]
                                # Где хранить snapshot
                #vb.customize ["modifyvm", :id, "--snapshotfolder", "D:\\test"]
                # Еще один способ сменить название VM в Vbox GUI
                #vb.customize ["modifyvm", :id, "--name", "Gangnam Style"]
            end
        end
    end
end
