
##Introduction of Vagrant

Vagrant - the command line utility for managing the lifecycle of virtual machines
Vagrant provides easy to configure, reproducible, and portable work environments built on top of industry-standard technology 
and controlled by a single consistent workflow to help maximize the productivity and flexibility of you and your team. 
To achieve its magic, Vagrant stands on the shoulders of giants. Machines are provisioned on top of VirtualBox, VMware, AWS, or any other provider. 
Then, industry-standard provisioning tools such as shell scripts, Chef, or Puppet, can be used to automatically install and configure software on the machine.


## Docker Vs Vagrant

## Docker
                   1) Virtualization type : Linux container 
		   2) Resource isolation  : Week
		   3) OS                  : Linux
		   4) Starting time       : Seconds
		   5) Building Image Time : Short 
		   6) Size                : 100M+

## Vagrant
		   1) Virtualization type : Virtual machine
		   2) Resource isolation  : Strong
		   3) OS                  : Linux,Windows,MacOS
		   4) Starting time       : Minutes
		   5) Building Image Time : Long (10+ mins)
		   6) Size	 	  : 1G+
		   
##Vagrant Commands:

Vagrant has a built-in command for initializing a directory for usage with Vagrant. in which Vagrantfile created 
		
			$ mkdir vagrant_getting_started
			$ cd vagrant_getting_started
			$ vagrant init


## Boxes
Vagrant uses a base image to quickly clone a virtual machine. These base images are known as "boxes" in Vagrant, 
and specifying the box to use for your Vagrant environment is always the first step after creating a new Vagrantfile.

## Installing a box

			$ vagrant box add hashicorp/precise64

Open the Vagrantfile and change the contents to the following:
			
			Vagrant.configure("2") do |config|
			  config.vm.box = "hashicorp/precise64"
			end

## UP AND SSH

It is time to boot your first Vagrant environment. Run the following from your terminal:

			$ vagrant up
			$ vagrant ssh

## Synced folders

By default, Vagrant shares your project directory (remember, that is the one with the Vagrantfile) to the /vagrant directory in your guest machine.


## PORT FORWARDING

One option is to use port forwarding. Port forwarding allows you to specify ports on the guest machine to share via a port on the host machine. 
This allows you to access a port on your own machine, but actually have all the network traffic forwarded to a specific port on the guest machine.
Let us setup a forwarded port so we can access Apache in our guest. Doing so is a simple edit to the Vagrantfile, which now looks like this:

			Vagrant.configure("2") do |config|
			  config.vm.box = "hashicorp/precise64"
			  config.vm.provision :shell, path: "bootstrap.sh"
			  config.vm.network :forwarded_port, guest: 80, host: 4567
			end

Run a vagrant reload or vagrant up (depending on if the machine is already running) so that these changes can take effect.
Once the machine is running again, load http://127.0.0.1:4567 in your browser. You should see a web page that is being served from the virtual machine that was automatically setup by Vagrant


## Teardown
        
			1) Suspend VM but memory still using by VM
		        $vagrant suspend
			
			2) Halt VM 
			
		        $vagrant halt
			
			3) Destroy VM which clear all disk space
			
			$vagrant destroy 
			
			4) The equivalent of running a halt followed by an up.( Usually used after modification of Vagrantfile)
			$vagrant reload
			
			5) This resumes a Vagrant managed machine that was previously suspended, perhaps with the suspend command.
			$vagrant resume
			
			
			

## Some more command of Vagrant

1)This command will tell you the state of all active Vagrant environments on the system for the currently logged in user.
	
			$vagrant global-status

2)The port command displays the full list of guest ports mapped to the host machine ports

			$ vagrant port
			22 (guest) => 2222 (host)
			80 (guest) => 8080 (host)
3) This will start an RDP client for a remote desktop session with the guest. This only works for Vagrant environments that support remote desktop, which is typically only Windows.

			$ vagrant rdp
			
4) The share command initializes a Vagrant Share session, allowing you to share your Vagrant environment with anyone in the world, enabling collaboration directly in your Vagrant environment in almost any network environment.
			
			$ vagrant share
			
5) This will output valid configuration for an SSH config file to SSH into the running Vagrant machine from ssh directly 
			
			$ vagrant ssh-config

6) To enable SSH sharing, simply supply the --ssh flag when calling vagrant share.
            
			$vagrant share --ssh
			
7)vagrant connect command gives the connecting person a static IP they can use to communicate to the shared Vagrant environment.
        
		        $ vagrant connect
			 
8) Vagrant VM debug 

	        	$vagrant up --debug &> vagrant.log

