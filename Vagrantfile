# Create vagrant box running ubuntu 16.04
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: 8080, host: 8080, auto_correct: true
  config.vm.network "forwarded_port", guest: 50000, host: 50000, auto_correct: true
end

# Configure VirtualBox  VM settings
Vagrant.configure("2") do |config|
 config.vm.provider "virtualbox" do |vb|
   vb.memory = "4096"
   vb.cpus = "2"
 end
end

# Install docker and pull the jenkins image
Vagrant.configure("2") do |config|
  config.vm.provision "docker",
     images: ["jenkins"]
end 


# Create Jenkins home and run the container
$script = <<-SCRIPT
sudo mkdir -p /var/jenkins_home
sudo chown -R 1000:1000 /var/jenkins_home/
docker run -p 8080:8080 -p 50000:50000 -v /var/jenkins_home:/var/jenkins_home --name jenkins -d jenkins
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: $script
end


