BOX_NAME = ENV['BOX_NAME'] || "ubuntu-raring"

BOX_URI = ENV['BOX_URI'] || "http://cloud-images.ubuntu.com/vagrant/raring/current/raring-server-cloudimg-amd64-vagrant-disk1.box"

FORWARD_DOCKER_PORTS = ENV['FORWARD_DOCKER_PORTS']

# Providers were added on Vagrant >= 1.1.0
Vagrant::VERSION >= "1.1.0" and Vagrant.configure("2") do |config|

  if Dir.glob("#{File.dirname(__FILE__)}/.vagrant/machines/default/*/id").empty?


    pkg_cmd = "wget -O- https://gist.github.com/erikj/6203151/raw/ubuntu-downsize.sh | sudo sh;"
    pkg_cmd << "wget -O- https://gist.github.com/erikj/6203151/raw/add.sh | sudo sh;"
    pkg_cmd << "wget -O- https://gist.github.com/erikj/6203151/raw/vbox.sh | sudo sh;"

    config.vm.provision :shell, :inline => pkg_cmd
  end

  # http://docs.vagrantup.com/v2/synced-folders/nfs.html
  config.vm.synced_folder '.', '/vagrant'

  config.vm.provider :virtualbox do |vb|
    vb.name = 'vagrant-docker-raring'
    config.vm.box = BOX_NAME
    config.vm.box_url = BOX_URI
  end
end

if !FORWARD_DOCKER_PORTS.nil?
  Vagrant::VERSION >= "1.1.0" and Vagrant.configure("2") do |config|
    (49000..49900).each do |port|
      config.vm.network :forwarded_port, :host => port, :guest => port
    end
  end
end
