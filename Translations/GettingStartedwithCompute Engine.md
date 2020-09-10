# Lab: 
Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives
In this lab, you will learn how to perform the following tasks:

- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

- Create a Compute Engine virtual machine using the gcloud command-line interface.

- Connect between the two instances.

## Steps
1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

	gcloud compute instances create "my-vm-1" --zone=us-central1-c --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190326" --subnet "default" --tags=http-server

	gcloud compute firewall-rules create allow-http --action=ALLOW --direction=INGRESS --rules=tcp:80  --target-tags=http-server

2. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

gcloud config set compute/zone us-central1-b

gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

3. Connect between the two instances.

	a. Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
		- connect to my-vm-2
			gcloud compute ssh my-vm-2
		- ping my-vm-1 from my-vm-2
			ping -c 4 my-vm-1

		- Use the ssh command to open a command prompt on my-vm-1:
			gcloud compute ssh my-vm-1

		- At the command prompt on my-vm-1, install the Nginx web server:
			sudo apt-get update
			sudo apt-get install nginx-light -y

		- Use the nano text editor to add a custom message to the home page of the web server:
			sudo nano /var/www/html/index.nginx-debian.html

		- Add text like this, and replace YOUR_NAME with Oluwasegun:
			Hi from Oluwasegun

		- Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
			curl http://localhost/

		Result: 
		<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
Hi from Oluwasegun
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>
<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>
<p><em>Thank you for using nginx.</em></p>
</body>
</html>

		- To exit the command prompt on my-vm-1, execute this command:
			exit

		- To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
			curl http://my-vm-1/

		Result: 
		<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
Hi from Oluwasegun
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>
<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>
<p><em>Thank you for using nginx.</em></p>
</body>
</html>

	b.  To get the external IP of the my-vm-1: 
			gcloud compute instances list  --zones=us-central1-c

	c. 	Copy the External IP address for my-vm-1 and paste it into the address bar of a new browser tab. 
			
		result:
		Welcome to nginx!
Hi from Oluwasegun
If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

For online documentation and support please refer to nginx.org.
Commercial support is available at nginx.com.

Thank you for using nginx.


  