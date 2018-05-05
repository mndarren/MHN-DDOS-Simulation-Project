# MHN-DDOS-Simulation-Project
=====================================================
1. Purpose of MHN project
	```
	1) Practice MHN to confirm its 2 big benefits(deploy honeypots fast and automatedly collect and summarize honeypot info).
	2) Simulate DDOS attack pattern.
	```
2. Architecture
	```
	Locally perform the experiment via 5 VMs
	```
	![alt Arthitecture](https://github.com/mndarren/MHN-DDOS-Simulation-Project/blob/master/resources/MHN_architecture.png)
3. How to deploy architecture planning
	```
	1)	Install VMware Workstation 12 on Windows 10;
	2)	Create 2 VMs and install VMware ESXi 6 and Kali 4.14 respectively
	The VM to install VMware ESXi 6 is special one which becomes a sandbox. 	Another 3 VMs will be built in this sandbox.
	3)	Install vSphere Client 6
	The vSphere Client is used to control ESXi. The following snapshots will 	show how to use it to create VMs in the sandbox;
	4)	Create 3 VMs in sandbox and install Ubuntu 16 for each via vSphere Client
	Tip 1, After finishing installing Ubuntu for the first VM, create a template 	(.ova) file. The (.ova) file can be used to create another VMs very easy and 	very fast.
	Tip 2, After installing packages or modifying configuration, take a snapshot 	for the VM. If some operation accidentally results in something wrong in VM, 	it can easily restore the snapshot state.
	5)	Install MHN on 1 VM. The detail will be found at how to install MHN.
	6)	Install Conpot on another 2 VM
	This step is the easiest one, just one command run.
	7)	Change hostname to MHN on MHN VM, honey1 and honey2 for Conpot VMs
	The purpose for this step is to show clearly output. The detail is at How to 	change hostname.
	8)	Install LOIC on Kali
	This is the hard one. We have to use Kali because Linux will consume less 	resource than Windows. In order to run LOIC.exe (Windows application), we 	have to install a lot of packages and related dependencies.
	9)	Install HOIC on Windows 10
	```