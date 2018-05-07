MHN DDOS Simulation Project
=====================================================
Purpose
---------
1) Practice MHN to confirm its 2 big benefits(deploy honeypots fast and 
automatedly collect and summarize honeypot info).
2) Simulate DDOS attack pattern.

Architecture
-------------
Locally perform the experiment via 5 VMs<br/>
![mhn_architecture](https://user-images.githubusercontent.com/17918808/39680627-6451c626-5168-11e8-8f44-2afc4f7d66c5.png)

How to deploy architecture planning
------------------------------------
	```
	1) Install VMware Workstation 12 on Windows 10;
	2) Create 2 VMs and install VMware ESXi 6 and Kali 4.14 respectively
	   The VM to install VMware ESXi 6 is special one which becomes a sandbox.
	   Another 3 VMs will be built in this sandbox.
	3) Install vSphere Client 6
	   The vSphere Client is used to control ESXi. The following snapshots will
	   show how to use it to create VMs in the sandbox;
	4) Create 3 VMs in sandbox and install Ubuntu 16 for each via vSphere Client
	   Tip 1, After finishing installing Ubuntu for the first VM, create a template (.ova) file.
	   The (.ova) file can be used to create another VMs very easy and  very fast.
	   Tip 2, After installing packages or modifying configuration, take a snapshot for the VM.
	   If some operation accidentally results in something wrong in VM, it can easily restore
	   the snapshot state.
	5) Install MHN on 1 VM. The detail will be found at how to install MHN.
	6) Install Conpot on another 2 VM
	   This step is the easiest one, just one command run.
	7) Change hostname to MHN on MHN VM, honey1 and honey2 for Conpot VMs
	   The purpose for this step is to show clearly output. The detail is at How to change hostname.
	8) Install LOIC on Kali
	   This is the hard one. We have to use Kali because Linux will consume less resource than Windows.
	   In order to run LOIC.exe (Windows application), we have to install a lot of packages
	   and related dependencies.
	9) Install HOIC on Windows 10
	```
How to install LOIC in Kali (this is the hard part)
----------------------------------------------------
	```
	1) setup repository for Kali 
	   sudo nano /etc/apt/source-list
	   deb http://http.kali.org/kali kali-rolling main contrib non-free
	   deb http://httpredir.debian.org/debian jessie-backports main
	2) Update and upgrade Kali
	3) Install mono package and related packages
	4) Download LOIC.exe (https://sourceforge.net/projects/loic/)
	5) Open LOIC 
	   mono LOIC.exe
	```
How to install MHN on Ubuntu
-----------------------------
	```
	1) Install git
	   sudo apt-get install git -y
	2) Install MHN
	   cd /opt/
	   sudo git clone https://github.com/threatstream/mhn.git
	   cd mhn/
	3) Run script
	   sudo ./install.sh
	Note: install all dependencies if required.
	```
How to reset hostname on Ubuntu
---------------------------------
	```
	1) reset /etc/hostname
	2) reset /etc/hosts
	3) reboot
	```
How to install Hoenypot
------------------------
1) Run MHN firstly;
2) Open browser with MHN VM IP
3) From Deploy tag, choose Conpot and then deploy script command showsup.
4) Run the only command to commpletely install and configure Conpot onUbuntu.
5) After done installation, check it from MHN browser UI Sensors tag.<br/>
![HoneypotInstall](https://github.com/mndarrenMHN-DDOS-Simulation-Project/tree/master/resources/setup_2_honey.PNG)

How to simulate DDOS to Honeypot network
------------------------------------------
	```
	1) open browser to watch GUI of MHN;
	2) start HOIC attack from Win10;
	3) start LOIC attack from Kali;
	4) detect DDOS attacks from MHN GUI.
	```
	![alt Simulating](https://github.com/mndarren/MHN-DDOS-Simulation-Project/tree/master/resources/ddos_simulating.PNG)
	![alt Catch_Win10](https://github.com/mndarren/MHN-DDOS-Simulation-Project/tree/master/resources/catch_win10_ip.PNG)
	![alt Win10_IP](https://github.com/mndarren/MHN-DDOS-Simulation-Project/tree/master/resources/win10_ip.PNG)
	![alt MHN_summary](https://github.com/mndarren/MHN-DDOS-Simulation-Project/tree/master/resources/MHN_summary_attck.PNG)
Two wired things
-------------------
	```
	1) From Kali, we found 2 different IP addresses at the same time during DDOS attack.
	   Why can a VM contains 2 different IP addresses with only one network card?
	2) After stopping DDOS attack (close LOIC and HOIC), MHN still can detect DDOS attack keep going.
	   Why? Cache? Queue?
	```
	![alt Catch_Kali](https://github.com/mndarren/MHN-DDOS-Simulation-Project/tree/master/resources/catch_kali_attack.PNG)
	![alt Kali_IP](https://github.com/mndarren/MHN-DDOS-Simulation-Project/tree/master/resources/Kali_ip.PNG)
Evaluation and future work
---------------------------
	```
	1)	The whole experiment was completed successfully. We created five virtual machines,
		including two honeypot sensors -- using Conpot version, one attacker machine – Kali.
		About the attack tools, LOIC and HOIC were chosen to perform DDOS attacks.
	2)	As for simulating attack, two attackers come from Kali, another attacker from Windows 10.
		All attacks were detected by the two sensors. The MHN 	system works very well.
		MHN VM collected all information from the two sensors, analyzed the attacks information and show them on a browser.
	3)	The limitation about this project is that the whole experiment was simulated locally.
		If it can be done on cloud, that will show the attackers’ country, 	which will be better to test the MHN works.
		Another limitation is that we only simulate DDOS attack pattern. We also can attempt
		to perform other attack patterns in the future, such as SQL injection, XXS, password guessing.
	4)	Additionally, for honeypot version, we only used Conpot to complete this project.
		In the future we can try other honeypots versions, such as Snort, 	Wordpot, Shockpot.
	```