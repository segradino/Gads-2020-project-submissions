# Lab: 
Google Cloud Fundamentals: Getting Started with App Engine


## Objectives
In this lab, you learn how to perform the following tasks:

	- Initialize App Engine.

	- Preview an App Engine application running locally in Cloud Shell.

	- Deploy an App Engine application, so that others can reach it.

	- Disable an App Engine application, when you no longer want it to be visible.


## Steps
Preamble

	a. list the active account name with this command: 
		gcloud auth list

	Result: 
	Credentialed accounts:
 	- student-03-6c58501c9c82@qwiklabs.net

 	b. You can list the project ID with this command:
 		gcloud config list project

 	Result: 
 	[core]
	project = qwiklabs-gcp-03-124382e701d2

1.  Initialize an App Engine 
	a. Initialize your App Engine app with your project and choose its region: 
		gcloud app create --project=$DEVSHELL_PROJECT_ID

	b. Clone the source code repository for a sample application in the hello_world directory:
		git clone https://github.com/GoogleCloudPlatform/python-docs-samples

	c. Navigate to the source directory:
		cd python-docs-samples/appengine/standard_python3/hello_world

2.	Run Hello World application locally

	a. Execute the following command to download and update the packages list.
		sudo apt-get update

	b. Set up a virtual environment in which you will run your application. Python virtual environments are used to isolate package installations from the system.
		sudo apt-get install virtualenv
		virtualenv -p python3 venv

	c. Activate the virtual environment.
		source venv/bin/activate

	d. Navigate to your project directory and install dependencies.
		pip install  -r requirements.txt

	e. Run the application:
		python main.py

	f. Preview the result on a web browser

		Result:
		Hello World

3.	Deploy and run Hello World on App Engine
	a. Navigate to the source directory:
		cd ~/python-docs-samples/appengine/standard_python3/hello_world

	b. Deploy your Hello World application.
	## If prompted "Do you want to continue (Y/n)?", press Y and then Enter.
		gcloud app deploy 

	c. Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com
		gcloud app browse
	d. Copy and paste the URL into a new browser window.

		Result:
		Hello World

4. Disable the application
	a. 



	