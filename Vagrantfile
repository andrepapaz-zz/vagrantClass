Vagrant.configure("2") do |config|
    
    config.ssh.pty = true
    config.vm.box = "ubuntu_aws"
    config.vm.box_url = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"
    config.vm.define :web do |web_config|
        web_config.vm.network "private_network", ip: "192.168.50.10"
        web_config.vm.provision "shell", path: "manifests/bootstrap.sh"
        web_config.vm.provision "puppet" do |puppet|
        	puppet.manifest_file = "web.pp"
        end
        web_config.vm.provider :aws do |aws|
            aws.tags = { 'Name' => 'Teste'}
        end
    end
    config.vm.provider :aws do |aws, override|
    	aws.access_key_id = ''
    	aws.secret_access_key = ''

    	aws.keypair_name = "KeyPairLocal"
    	aws.ami = "ami-7379e31f"
        aws.instance_type = "t2.micro"
        aws.region = "sa-east-1"
    	aws.security_groups = ['webaccess']
    	
    	override.ssh.username = "ubuntu"
    	override.ssh.private_key_path = "KeyPairLocal.pem"
    end
end