# Lab: 
Creating Virtual Machines

## Objectives

In this lab, you learn how to perform the following tasks:

	- Create several standard VMs

	- Create advanced VMs


## Steps
1. Create a utility virtual machine
	gcloud beta compute --project=qwiklabs-gcp-03-8b1ac11de44c instances create create-vm-segz --zone=us-central1-c --machine-type=n1-standard-1 --subnet=default --no-address --image=debian-10-buster-v20200910 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=create-vm-segz 

2. Create a Windows virtual machine

	gcloud beta compute --project=qwiklabs-gcp-03-8b1ac11de44c instances create windows-instance --zone=europe-west2-a --machine-type=n1-standard-2 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --tags=http-server,https-server --image=windows-server-2016-dc-core-v20200813 --image-project=windows-cloud --boot-disk-size=100GB --boot-disk-type=pd-ssd --boot-disk-device-name=windows-instance 

##Firewall Rules for HTTP

gcloud compute --project=qwiklabs-gcp-03-8b1ac11de44c firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server

##Firewall Rules for HTTPs
gcloud compute --project=qwiklabs-gcp-03-8b1ac11de44c firewall-rules create default-allow-https --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:443 --source-ranges=0.0.0.0/0 --target-tags=https-server

3.	Create a custom virtual machine
	gcloud beta compute --project=qwiklabs-gcp-03-8b1ac11de44c instances create custom-instance-segz --zone=us-west1-b --machine-type=e2-custom-6-32768 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE  --image=debian-10-buster-v20200910 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=custom-instance-segz

4.	Connect via SSH to your custom VM
	gcloud compute ssh custom-instance-segz

	a. to see information about unused and used memory and swap space on your custom VM, run the following command:
		free

		Result: 
			total        used        free      shared  buff/cache   available
Mem:       32943924      220248    32591420        8496      132256    32389804
Swap:             0           0           0

	b. To see details about the RAM installed on your VM, run the following command:
		sudo dmidecode -t 17

		Result: 
		# dmidecode 3.2
		Getting SMBIOS data from sysfs.
		SMBIOS 2.4 present.
		Handle 0x7000, DMI type 17, 21 bytes
		Memory Device
        Array Handle: 0x0200
        Error Information Handle: Not Provided
        Total Width: 64 bits
        Data Width: 64 bits
        Size: 16384 MB
        Form Factor: DIMM
        Set: None
        Locator: DIMM 0
        Bank Locator: Not Specified
        Type: RAM
        Type Detail: Synchronous
		Handle 0x7001, DMI type 17, 21 bytes
		Memory Device
        Array Handle: 0x0200
        Error Information Handle: Not Provided
        Total Width: 64 bits
        Data Width: 64 bits
        Size: 16384 MB
        Form Factor: DIMM
        Set: None
        Locator: DIMM 1
        Bank Locator: Not Specified
        Type: RAM
        Type Detail: Synchronous

        c. To verify the number of processors, run the following command:
        	nproc

        	Result: 6

        d. To see details about the CPUs installed on your VM, run the following command:
        	lscpu

        	Result: 
        	Architecture:        x86_64
			CPU op-mode(s):      32-bit, 64-bit
			Byte Order:          Little Endian
			Address sizes:       46 bits physical, 48 bits virtual
			CPU(s):              6
			On-line CPU(s) list: 0-5
			Thread(s) per core:  2
			Core(s) per socket:  3
			Socket(s):           1
			NUMA node(s):        1
			Vendor ID:           GenuineIntel
			CPU family:          6
			Model:               79
			Model name:          Intel(R) Xeon(R) CPU @ 2.20GHz
			Stepping:            0
			CPU MHz:             2200.188
			BogoMIPS:            4400.37
			Hypervisor vendor:   KVM
			Virtualization type: full
			L1d cache:           32K
			L1i cache:           32K
			L2 cache:            256K
			L3 cache:            56320K
			NUMA node0 CPU(s):   0-5
			Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse s
			se2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq pni pc
			lmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dno
			wprefetch invpcid_single pti ssbd ibrs ibpb stibp fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm rdse
			ed adx smap xsaveopt arat md_clear arch_capabilities

		e. To exit the SSH terminal, run the following command:
			exit

