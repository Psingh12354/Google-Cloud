<h1 align=center><i><b>Google Cloud</b></i></h1>

<p align=center><img src="https://github.com/Psingh12354/Google-Cloud-/blob/main/Qwik.png" width=100 height=100></img></p>

<h3 align=center><i><b>Welcome! to the Qwicklab</b></i></h3>

### Go to qwiklab here [click me](https://google.qwiklabs.com/)

### About Navigation

The **Navigation menu** is an important component of the Cloud Console—it offers quick access to the platform's services and also outlines its offerings. If you scroll through the menu, you will see that there are seven categories of Google Cloud services:

- **Compute:** houses a variety of machine types that support any type of workload. The different computing options let you decide how involved you want to be with operational details and infrastructure amongst other things.
- **Storage:** data storage and database options for structured or unstructured, relational or non relational data.
- **Networking:** services that balance application traffic and provision security rules amongst other things.
- **Cloud Operations:** a suite of cross-cloud logging, monitoring, trace, and other service reliability tools.
- **Tools:** services for developers managing deployments and application build pipelines.
- **Big Data:** services that allow you to process and analyze large datasets.
- **Artificial Intelligence:** a suite of APIs that run specific artificial intelligence and machine learning tasks on Google Cloud.

### Terminal Open

To open a terminal on google cloud find the square on top right corner like this |>'| and click there

### Auth-list

To open the auth list type this command on terminal
```
gcloud auth list
```

### Types of Access Specifier

![](https://github.com/Psingh12354/Google-Cloud-/blob/main/Google.PNG)

### Text File

```
touch text.txt
```

### List the file

```
ls
```

### Read the cloud shell

```
README-cloudshell.txt  test.txt
```

### To _open_ the file in terminal

```
nano test.txt
```
### Process to come out from nano
Press
- Control + X
- Y
- Enter

### To _read_ the file in terminal

```
cat test.txt
```

<h2 align=center><i><b>Creating a Virtual Machiene</b></i></h2>

You can list the project ID with this command:

```
gcloud config list project
```

### output

```
[core]
project = qwiklabs-gcp-44776a13dea667a6
```

## Understanding Regions and Zones
Certain Compute Engine resources live in regions or zones. A region is a specific geographical location where you can run your resources. Each region has one or more zones. For example, the us-central1 region denotes a region in the Central United States that has zones ```us-central1-a```, ```us-central1-b```, ```us-central1-c```, and ```us-central1-f```.
![](https://github.com/Psingh12354/Google-Cloud/blob/main/Region.PNG)

Resources that live in a zone are referred to as zonal resources. Virtual machine Instances and persistent disks live in a zone. To attach a persistent disk to a virtual machine instance, both resources must be in the same zone. Similarly, if you want to assign a static IP address to an instance, the instance must be in the same region as the static IP.

### Create a new instance from the Cloud Console

In this section, you'll learn how to create new pre-defined machine types with Compute Engine from the Cloud Console.

In the Cloud Console, on the top left of the screen, select **Navigation menu > Compute Engine > VM Instances:**

![](https://github.com/Psingh12354/Google-Cloud/blob/main/Instance.PNG)
This may take a minute to initialize for the first time.

To create a new instance, click **Create**.

![](https://github.com/Psingh12354/Google-Cloud/blob/main/create.PNG)

There are many parameters you can configure when creating a new instance. Use the following for this lab:
![](https://github.com/Psingh12354/Google-Cloud/blob/main/instance1.PNG)
![](https://github.com/Psingh12354/Google-Cloud/blob/main/instance2.PNG)

Click **Create.**

Wait for it to finish - it shouldn't take more than a minute.

Once finished, you should see the new virtual machine in the **VM Instances** page.

To SSH into the virtual machine, click on **SSH** on the right hand side. This launches a SSH client directly from your browser.

![](https://github.com/Psingh12354/Google-Cloud/blob/main/SSh.PNG)

## Install a NGINX web server
Now you'll install NGINX web server, one of the most popular web servers in the world, to connect your virtual machine to something.

Once SSH'ed, get ```root``` access using ```sudo```:
```
sudo su -
```
As the ```root``` user, update your OS:
```
apt-get update
```
(Output)
```
Get:1 http://security.debian.org stretch/updates InRelease [94.3 kB]
Ign http://deb.debian.org strech InRelease
Get:2 http://deb.debian.org strech-updates InRelease [91.0 kB]
...
```
### Install NGINX:
```
apt-get install nginx -y
```
(Output)
```
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
...
```
### Check that NGINX is running:
```
ps auwx | grep nginx
```
(Output)
```
root      2330  0.0  0.0 159532  1628 ?        Ss   14:06   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data  2331  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
www-data  2332  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
root      2342  0.0  0.0  12780   988 pts/0    S+   14:07   0:00 grep nginx
```
Awesome! To see the web page, go to the Cloud Console and click the External IP link of the virtual machine instance. You can also see the web page by adding the ```External``` IP to ```http://EXTERNAL_IP/``` in a new browser window or tab.
![](https://github.com/Psingh12354/Google-Cloud/blob/main/SSh.PNG)

You should see this default web page:

![](https://github.com/Psingh12354/Google-Cloud/blob/main/ngins.PNG)

To check your progress in this lab, click Check my progress below. A checkmark means you're on track.

### Create a new instance with gcloud

Rather than using the Cloud Console to create a virtual machine instance, you can use the command line tool gcloud, which is pre-installed in Google Cloud Shell. Cloud Shell is a Debian-based virtual machine loaded with all the development tools you'll need (gcloud, git, and others) and offers a persistent 5GB home directory.

In the Cloud Shell, create a new virtual machine instance from the command line using ```gcloud```:
```
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone us-central1-c
```
(Output)
```
Created [...gcelab2].
NAME     ZONE           MACHINE_TYPE  ...    STATUS
gcelab2  us-central1-c  n1-standard-2 ...    RUNNING
```
The instance created has these default values:

- The latest Debian 9 (stretch) image.
- The n1-standard-2 machine type. In this lab you can select one of these other machine types if you'd like: n1-highmem-4 or n1-highcpu-4. When you're working on a project outside of Qwiklabs, you can also specify a custom machine type.
- A root persistent disk with the same name as the instance; the disk is automatically attached to the instance.
Run ```gcloud compute instances create --help``` to see all the defaults.
```
Note: You can set the default region and zones that gcloud uses if you are always working within one region/zone and you don't want to append the --zone flag every time. Do this by running these commands :

gcloud config set compute/zone ...

gcloud config set compute/region ...
```
To exit help, press **Ctrl+c**.

Check out your instances. Select **Navigation menu > Compute Engine > VM instances.** You should see the 2 instances you created in this lab.

![](https://github.com/Psingh12354/Google-Cloud/blob/main/SSh.PNG)

a new gcelab added here

Finally, you can SSH into your instance using ```gcloud``` as well. Make sure you add your zone, or omit the ```--zone``` flag if you've set the option globally:
```
gcloud compute ssh gcelab2 --zone us-central1-c
```
(Output)
```
WARNING: The public SSH key file for gcloud does not exist.
WARNING: The private SSH key file for gcloud does not exist.
WARNING: You do not have an SSH key for gcloud.
WARNING: [/usr/bin/ssh-keygen] will be executed to generate a key.
This tool needs to create the directory
[/home/gcpstaging306_student/.ssh] before being able to generate SSH
Keys.
```
Now you'll type **Y** to continue.
```
Do you want to continue? (Y/n)
```
**Enter** through the passphrase section to leave the passphrase empty.
```
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase)
```
After connecting, you disconnect from SSH by exiting from the remote shell:
```
exit
```

<h1 align=center><i><b>Getting Started with Cloud Shell & gcloud</b></i></h1>

### Project Id

```
gcloud compute project-info describe --project <your_project_ID>
```

## Setting environment variables

Environment variables are variables that define your environment. Define your own variables and save yourself time when writing scripts that contain APIs or executables.

Make a couple of environment variables:

```
export PROJECT_ID=<your_project_ID>
```

Set your ZONE environment variable (use the value for zone from the earlier command):

```
export ZONE=<your_zone>
```

Verify that your variables were set properly:

```
echo $PROJECT_ID
echo $ZONE
```

## Create a virtual machine with gcloud

Create a new virtual machine instance using ```gcloud```. In the following command you'll use:

```gcloud compute``` which enables you to easily manage your Compute Engine resources in a friendlier format than using the Compute Engine API.
```instances create``` creates a new instance.
Run the following to create your vm:

```
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone $ZONE
```
(Output)

![](https://github.com/Psingh12354/Google-Cloud/blob/main/outputgit.png)

### If you got a error : 

```
ERROR: (gcloud.compute.instances.create) The required property [project] is not currently set.
You may set it for your current workspace by running:
  $ gcloud config set project VALUE
or it can be set temporarily by the environment variable [CLOUDSDK_CORE_PROJECT]
student_03_c58135da19e3@cloudshell:~$
```

### Use this :

```
gcloud config set command <Project_ID> //command can be project or something else with id 
like -:: 
gcloud config set  project qwiklabs-gcp-00-4b2e8b079910

```

- The name of the vm is "gcelab2",
- You're using the ```--machine-type``` flag to specify the machine type as "n1-standard-2"
- You're using the ```--zone``` flag to specify that it gets created in the zone you defined with your environment variable.

## Using gcloud commands

```gcloud``` offers simple usage guidelines that are available by adding the ```-h```flag (for help) onto the end of any ```gcloud``` invocation.

Run the following command in Cloud Shell:

```
gcloud -h
```

More verbose help can be obtained by appending ```--help``` flag, or executing ```gcloud``` help command. Run the following in Cloud Shell:
```
gcloud config --help
```
Use the **Enter** key or the **Spacebar** to scroll through the help content.

Type q to exit the content.

Now run the following command:

```
gcloud help config
```

You can see that the ```gcloud config --help``` and ```gcloud help config``` commands are equivalent. Both give long, detailed help.

[gcloud Global Flags](https://cloud.google.com/sdk/gcloud/reference/) govern the behavior of commands on a per-invocation level. Flags override any values set in SDK properties.

View the list of configurations in your environment:

```
gcloud config list
```

To check how other properties are set, see all properties by calling:

```
gcloud config list --all
```

List your components:

```
gcloud components list
```

Here you will see what components are ready for you to use in this lab. Next you'll install a new component.

## Auto-completion

```gcloud interactive``` has auto prompting for commands and flags, and displays inline help snippets in the lower section as the command is typed.

Static information, like command and sub-command names, and flag names and enumerated flag values, are auto-completed using dropdown menus.

Install the beta components:

```
sudo apt-get install google-cloud-sdk
```

Enter the ```gcloud interactive``` mode:

```
gcloud beta interactive
```

When using the interactive mode, click on the **Tab** key to complete file path and resource arguments. If a dropdown menu appears, use the **Tab** key to move through the list, and the **Space bar** to select your choice.

Try it out! Start typing the following command, using auto-complete to finish the command:

```
gcloud compute instances describe <your_vm>
```

Across the bottom of Cloud Shell you can see the shortcut to toggle this feature. Try out the F2 toggle:

F2:help:STATE Toggles the active help section, ON when enabled, OFF when disabled.

## SSH into your vm instance
```gcloud compute``` makes connecting to your instances easy. The ```gcloud``` compute ssh command provides a wrapper around ```SSH```, which takes care of authentication and the mapping of instance name to IP address.

Use ```gcloud compute ssh``` to SSH into your vm:

```
gcloud compute ssh gcelab2 --zone $ZONE
```

(Output)

```
WARNING: The public SSH key file for gcloud does not exist.
WARNING: The private SSH key file for gcloud does not exist.
WARNING: You do not have an SSH key for gcloud.
WARNING: [/usr/bin/ssh-keygen] will be executed to generate a key.
This tool needs to create the directory
[/home/gcpstaging306_student/.ssh] before being able to generate SSH Keys.
```

Type "Y" to continue:

```
Do you want to continue? (Y/n)
```

Press the **Enter** key through the passphrase section to leave the passphrase empty.

```
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase)
```

You don't need to do anything here, so disconnect from SSH by exiting from the remote shell by typing "exit":

```
exit
```
You should be back at your project's command prompt.

## Use the Home directory
Now try out your Home directory. The contents of your Cloud Shell Home directory persists across projects between all Cloud Shell sessions, even after the virtual machine terminates and is restarted.

Change your current working directory:

```
cd $HOME
```

Open your ```.bashrc``` configuration file using ```vi``` text editor:

```
vi ./.bashrc
```

The editor opens and displays the contents of the file. Press the ```ESC``` key and then ```:wq``` to exit the editor.


<h1><i><b>Kubernetes Engine: Qwik Start</b></i></h1>

You can list the active account name with this command:

```
gcloud auth list
```

(Output)

```
Credentialed accounts:
 - <myaccount>@<mydomain>.com (active)
```
(Example output)
```
Credentialed accounts:
 - google1623327_student@qwiklabs.net
```
You can list the project ID with this command:
```
gcloud config list project
```
(Output)
```
[core]
project = <project_ID>
```
(Example output)
```
[core]
project = qwiklabs-gcp-44776a13dea667a6
```

## Setting a default compute zone
Your compute zone is an approximate regional location in which your clusters and their resources live. For example, us-central1-a is a zone in the us-central1 region.

Start a new session in Cloud Shell and run the following command to set your default compute zone to us-central1-a:

gcloud config set compute/zone us-central1-a

You receive the following output:

Updated property [compute/zone].
Creating a Kubernetes Engine cluster
A cluster consists of at least one cluster master machine and multiple worker machines called nodes. Nodes are Compute Engine virtual machine (VM) instances that run the Kubernetes processes necessary to make them part of the cluster.

To create a cluster, run the following command, replacing [CLUSTER-NAME] with the name you choose for the cluster (for example my-cluster). Cluster names must start with a letter, end with an alphanumeric, and cannot be longer than 40 characters.

```
gcloud container clusters create [CLUSTER-NAME]
```
You can ignore any warnings in the output. It might take several minutes to finish creating the cluster. Soon after you should receive a similar output:
```
NAME        LOCATION       ...   NODE_VERSION  NUM_NODES  STATUS
my-cluster  us-central1-a  ...   1.15.12-gke.2  3          RUNNING
```

## Creating a Kubernetes Engine cluster

A [cluster](https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-architecture) consists of at least one cluster master machine and multiple worker machines called nodes. Nodes are [Compute Engine virtual machine (VM) instances](https://cloud.google.com/compute/docs/instances/) that run the Kubernetes processes necessary to make them part of the cluster.

To create a cluster, run the following command, replacing ```[CLUSTER-NAME]``` with the name you choose for the cluster (for example ```my-cluster```). Cluster names must start with a letter, end with an alphanumeric, and cannot be longer than 40 characters.

### Important

```
gcloud config set  project qwiklabs-gcp-00-4b2e8b079910
```

```
gcloud container clusters create [CLUSTER-NAME]
```

You can ignore any warnings in the output. It might take several minutes to finish creating the cluster. Soon after you should receive a similar output:

```
NAME        LOCATION       ...   NODE_VERSION  NUM_NODES  STATUS
my-cluster  us-central1-a  ...   1.15.12-gke.2  3          RUNNING
```

## Get authentication credentials for the cluster

After creating your cluster, you need to get authentication credentials to interact with the cluster.

To authenticate the cluster run the following command, replacing ```[CLUSTER-NAME]``` with the name of your cluster:

```
gcloud container clusters get-credentials [CLUSTER-NAME]
```

You should receive a similar output:
```
Fetching cluster endpoint and auth data.
kubeconfig entry generated for my-cluster.
```

## Deploying an application to the cluster
Now that you have created a cluster, you can deploy a containerized application to it. For this lab you'll run ```hello-app``` in your cluster.

Kubernetes Engine uses Kubernetes objects to create and manage your cluster's resources. Kubernetes provides the Deployment object for deploying stateless applications like web servers. Service objects define rules and load balancing for accessing your application from the Internet.

Run the following [kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create) command in Cloud Shell to create a new Deployment ```hello-server``` from the ```hello-app```container image:

```
kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
```

You should receive the following output:
```
deployment.apps/hello-server created
```

This Kubernetes command creates a Deployment object that represents hello-server. In this case, --image specifies a container image to deploy. The command pulls the example image from a Google Container Registry bucket. gcr.io/google-samples/hello-app:1.0 indicates the specific image version to pull. If a version is not specified, the latest version is used.

Now create a Kubernetes Service, which is a Kubernetes resource that lets you expose your application to external traffic, by running the following kubectl expose command:

kubectl expose deployment hello-server --type=LoadBalancer --port 8080

In this command:

- ```--port specifies``` the port that the container exposes.
- ```type="LoadBalancer"``` creates a Compute Engine load balancer for your container.
You should receive the following output:

```
service/hello-server exposed
```
Inspect the hello-server Service by running kubectl get:
```
kubectl get 
```
You should receive a similar output:

![](https://github.com/Psingh12354/Google-Cloud/blob/main/out1.png)

```
Note: It might take a minute for an external IP address to be generated. Run the above command again if the EXTERNAL-IP column is in "pending" status.
```
From this command's output, copy the Service's external IP address from the ```EXTERNAL IP``` column.

View the application from your web browser using the external IP address with the exposed port:

```
http://[EXTERNAL-IP]:8080
```
Your page should resemble the following:

![](https://github.com/Psingh12354/Google-Cloud/blob/main/out2.png)

## Clean Up

Run the following to delete the cluster:

```
gcloud container clusters delete [CLUSTER-NAME]
```

When prompted, type Y to confirm. Deleting the cluster can take a few minutes. For more information on deleted Google Kubernetes Engine clusters, view the documentation.

Click Check my progress to 

<h1 align=center><b><i>Set Up Network and HTTP Load Balancers</i></b></h1>

## Activate Cloud Shell

You can list the active account name with this command:

```
gcloud auth list
```

(Output)

```
Credentialed accounts:
 - <myaccount>@<mydomain>.com (active)
 ```
 
(Example output)

```
Credentialed accounts:
 - google1623327_student@qwiklabs.net
```

You can list the project ID with this command:

```
gcloud config list project
```

(Output)

```
[core]
project = <project_ID>
```

(Example output)

```
[core]
project = qwiklabs-gcp-44776a13dea667a6
```

## Set the default region and zone for all resources
In Cloud Shell, set the default zone:

```
gcloud config set compute/zone us-central1-a
```

Set the default region:

```
gcloud config set compute/region us-central1
```

## Create multiple web server instances
To simulate serving from a cluster of machines, create a simple cluster of Nginx web servers to serve static content using Instance Templates and Managed Instance Groups. Instance Templates define the look of every virtual machine in the cluster (disk, CPUs, memory, etc). Managed Instance Groups instantiate a number of virtual machine instances using the Instance Template.

To create the Nginx web server clusters, create the following:

- A startup script to be used by every virtual machine instance to setup Nginx server upon startup
- An instance template to use the startup script
- A target pool
- A managed instance group using the instance template

Still in Cloud Shell, create a startup script to be used by every virtual machine instance. This script sets up the Nginx server upon startup:

```
cat << EOF > startup.sh
#! /bin/bash
apt-get update
apt-get install -y nginx
service nginx start
sed -i -- 's/nginx/Google Cloud Platform - '"\$HOSTNAME"'/' /var/www/html/index.nginx-debian.html
EOF
```

Create an instance template, which uses the startup script:

```
gcloud compute instance-templates create nginx-template \
         --metadata-from-file startup-script=startup.sh
```

(Output)

```
Created [...].
NAME           MACHINE_TYPE  PREEMPTIBLE CREATION_TIMESTAMP
nginx-template n1-standard-1             2015-11-09T08:44:59.007-08:00
```

Create a target pool. A target pool allows a single access point to all the instances in a group and is necessary for load balancing in the future steps.

```
gcloud compute target-pools create nginx-pool
```

(Output)

```
Created [...].
NAME       REGION       SESSION_AFFINITY BACKUP HEALTH_CHECKS
nginx-pool us-central1
```

Create a managed instance group using the instance template:

```
gcloud compute instance-groups managed create nginx-group \
         --base-instance-name nginx \
         --size 2 \
         --template nginx-template \
         --target-pool nginx-pool
```

(Output)

```
Created [...].
NAME         LOCATION       SCOPE  BASE_INSTANCE_NAME  SIZE  TARGET_SIZE  INSTANCE_TEMPLATE  AUTOSCALED
nginx-group  us-central1-a  zone   nginx               0     2            nginx-template     no
```

This creates 2 virtual machine instances with names that are prefixed with ```nginx-```. This may take a couple of minutes.

List the compute engine instances and you should see all of the instances created:

```
gcloud compute instances list
```

(Output)

```
NAME       ZONE           MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP EXTERNAL_IP    STATUS
nginx-7wvi us-central1-a n1-standard-1             10.240.X.X  X.X.X.X           RUNNING
nginx-9mwd us-central1-a n1-standard-1             10.240.X.X  X.X.X.X           RUNNING
```

Now configure a firewall so that you can connect to the machines on port 80 via the ```EXTERNAL_IP``` addresses:

gcloud compute firewall-rules create www-firewall --allow tcp:80

You should be able to connect to each of the instances via their external IP addresses via ```http://EXTERNAL_IP/``` shown as the result of running the previous command.

## Create a Network Load Balancer
Network load balancing allows you to balance the load of your systems based on incoming IP protocol data, such as address, port, and protocol type. You also get some options that are not available, with HTTP(S) load balancing. For example, you can load balance additional TCP/UDP-based protocols such as SMTP traffic. And if your application is interested in TCP-connection-related characteristics, network load balancing allows your app to inspect the packets, where HTTP(S) load balancing does not.

Create an L4 network load balancer targeting your instance group:

```
gcloud compute forwarding-rules create nginx-lb \
         --region us-central1 \
         --ports=80 \
         --target-pool nginx-pool
```

(Output)

```
Created [https://www.googleapis.com/compute/v1/projects/...].
```

List all Compute Engine forwarding rules in your project.

```
gcloud compute forwarding-rules list
```

(Output)

```
NAME     REGION       IP_ADDRESS     IP_PROTOCOL TARGET
nginx-lb us-central1 X.X.X.X        TCP         us-central1/targetPools/nginx-pool
```

You can then visit the load balancer from the browser http://IP_ADDRESS/ where IP_ADDRESS is the address shown as the result of running the previous command.

## Create a HTTP(s) Load Balancer
HTTP(S) load balancing provides global load balancing for HTTP(S) requests destined for your instances. You can configure URL rules that route some URLs to one set of instances and route other URLs to other instances. Requests are always routed to the instance group that is closest to the user, provided that group has enough capacity and is appropriate for the request. If the closest group does not have enough capacity, the request is sent to the closest group that does have capacity.

First, create a health check. Health checks verify that the instance is responding to HTTP or HTTPS traffic:

```
gcloud compute http-health-checks create http-basic-check
```

(Output)

```
Created [https://www.googleapis.com/compute/v1/projects/...].
NAME             HOST PORT REQUEST_PATH
http-basic-check      80   /
```

Define an HTTP service and map a port name to the relevant port for the instance group. Now the load balancing service can forward traffic to the named port:

```
gcloud compute instance-groups managed \
       set-named-ports nginx-group \
       --named-ports http:80
```

(Output)

```
Updated [https://www.googleapis.com/compute/v1/projects/...].
```

Create a backend service:

```
gcloud compute backend-services create nginx-backend \
      --protocol HTTP --http-health-checks http-basic-check --global
```

(Output)

```
Created [https://www.googleapis.com/compute/v1/projects/...].
NAME          BACKENDS PROTOCOL
nginx-backend          HTTP
```

Add the instance group into the backend service:

```
gcloud compute backend-services add-backend nginx-backend \
    --instance-group nginx-group \
    --instance-group-zone us-central1-a \
    --global
```

(Output)

```
Updated [https://www.googleapis.com/compute/v1/projects/...].
```

Create a default URL map that directs all incoming requests to all your instances:

```
gcloud compute url-maps create web-map \
    --default-service nginx-backend
```

(Output)

```
Created [https://www.googleapis.com/compute/v1/projects/...].
NAME    DEFAULT_SERVICE
Web-map nginx-backend
```

Create a target HTTP proxy to route requests to your URL map:

```
gcloud compute target-http-proxies create http-lb-proxy \
    --url-map web-map
```

(Output)

```
Created [https://www.googleapis.com/compute/v1/projects/...].
NAME          URL_MAP
http-lb-proxy web-map
```

Create a global forwarding rule to handle and route incoming requests. A forwarding rule sends traffic to a specific target HTTP or HTTPS proxy depending on the IP address, IP protocol, and port specified. The global forwarding rule does not support multiple ports.

```
gcloud compute forwarding-rules create http-content-rule \
        --global \
        --target-http-proxy http-lb-proxy \
        --ports 80
```

(Output)

```
Created [https://www.googleapis.com/compute/v1/projects/...].
```

After creating the global forwarding rule, it can take several minutes for your configuration to propagate.

```
gcloud compute forwarding-rules list
```
(Output)

```
NAME              REGION IP_ADDRESS    IP_PROTOCOL TARGET
http-content-rule        X.X.X.X       TCP         http-lb-proxy
nginx-lb   us-central1  X.X.X.X       TCP         us-central1/....
```

Take note of the http-content-rule IP_ADDRESS for the forwarding rule.

From the browser, you should be able to connect to ```http://IP_ADDRESS/```. It may take three to five minutes. If you do not connect, wait a minute then reload the browser.

<h1 align=center><b><i>Getting Started: Create and Manage Cloud Resources: Challenge Lab</i></b></h1>

## Challenge scenario
You have started a new role as a Junior Cloud Engineer for Jooli Inc. You are expected to help manage the infrastructure at Jooli. Common tasks include provisioning resources for projects.

You are expected to have the skills and knowledge for these tasks, so don't expect step-by-step guides to be provided.

Some Jooli Inc. standards you should follow:

Create all resources in the default region or zone, unless otherwise directed.
Naming is normally team-resource, e.g. an instance could be named nucleus-webserver1
Allocate cost effective resource sizes. Projects are monitored and excessive resource use will result in the containing project's termination (and possibly yours), so beware. This is the guidance the monitoring team is willing to share; unless directed use f1-micro for small Linux VMs and n1-standard-1 for Windows or other applications such as Kubernetes nodes.
Your challenge
As soon as you sit down at your desk and open your new laptop you receive several requests from the Nucleus team. Read through each description, then create the resources.

## Task 1: Create a project jumphost instance

We will use this instance to perform maintenance for the project.

Make sure you:

name the instance ```nucleus-jumphost```
use the machine type of f1-micro
use the default image type (Debian Linux)

## Solution :

```
gcloud compute instances create nucleus-jumphost \
                  --network nucleus-vpc \
                  --zone us-east1-b  \
                  --machine-type f1-micro  \
                  --image-family debian-9  \
                  --image-project debian-cloud \
                  --scopes cloud-platform \
                  --no-address
                  
                  Or 
                  
Navigation menu > Compute engine > VM Instance                  
```

## Task 2: Create a Kubernetes service cluster

```
You have a limit to the resources you are allowed to create in your project, if you don't get the result you expected please delete the cluster before you create another cluster or the lab might exit and you might get banned.
The team is building an application that will use a service. This service will run on Kubernetes. You need to:
```

- Create a cluster (in the us-east1-b zone) to host the service
- Use the Docker container hello-app (`gcr.io/google-samples/hello-app:2.0`) as a place holder, the team will replace the container with their own work later
- Expose the app on port 8080

### Solution(Each step one by one)
```
Create a Kubernetes service cluster

gcloud config set compute/zone us-east1-b

gcloud container clusters create nucleus-webserver1

gcloud container clusters get-credentials nucleus-webserver1

kubectl create deployment hello-app --image=gcr.io/google-samples/hello-app:2.0

kubectl expose deployment hello-app --type=LoadBalancer --port 8080

kubectl get service 
```

## Task 3: Setup an HTTP load balancer

We will serve the site via nginx web servers, but we want to ensure we have a fault tolerant environment, so please create an HTTP load balancer with a managed instance group of **two nginx web servers**. Use the following to configure the web servers, the team will replace this with their own configuration later.

```
You have a limit to the resources you are allowed to create in your project, so do not create more than two instances in your managed instance group or the lab might exit and you might get banned.
```

```
cat << EOF > startup.sh
#! /bin/bash
apt-get update
apt-get install -y nginx
service nginx start
sed -i -- 's/nginx/Google Cloud Platform - '"\$HOSTNAME"'/' /var/www/html/index.nginx-debian.html
EOF
```

You need to:

- Create an instance template
- Create a target pool
- Create a managed instance group
- Create a firewall rule to allow traffic (80/tcp)
- Create a health check
- Create a backend service and attach the manged instance group
- Create a URL map and target HTTP proxy to route requests to your URL map
- Create a forwarding rule

 ### Solution(Step by step) : 
 
 ```
 1 .Create an instance template :

gcloud compute instance-templates create nginx-template \
--metadata-from-file startup-script=startup.sh

2 .Create a target pool :

gcloud compute target-pools create nginx-pool
```

**Note :** Press No and select region which is given in you first question.

```
3 .Create a managed instance group :

gcloud compute instance-groups managed create nginx-group \
--base-instance-name nginx \
--size 2 \
--template nginx-template \
--target-pool nginx-pool

gcloud compute instances list

4 .Create a firewall rule to allow traffic (80/tcp) :

gcloud compute firewall-rules create www-firewall --allow tcp:80

gcloud compute forwarding-rules create nginx-lb \
--region us-east1 \
--ports=80 \
--target-pool nginx-pool

gcloud compute forwarding-rules list

5 .Create a health check :

gcloud compute http-health-checks create http-basic-check

gcloud compute instance-groups managed \
set-named-ports nginx-group \
--named-ports http:80

6 .Create a backend service and attach the manged instance group :

gcloud compute backend-services create nginx-backend \
--protocol HTTP --http-health-checks http-basic-check --global

gcloud compute backend-services add-backend nginx-backend \
--instance-group nginx-group \
--instance-group-zone us-east1-b \
--global

7 .Create a URL map and target HTTP proxy to route requests to your URL map :

gcloud compute url-maps create web-map \
--default-service nginx-backend

gcloud compute target-http-proxies create http-lb-proxy \
--url-map web-map

8 .Create a forwarding rule :

gcloud compute forwarding-rules create http-content-rule \
--global \
--target-http-proxy http-lb-proxy \
--ports 80

gcloud compute forwarding-rules list
```
![](https://github.com/Psingh12354/Google-Cloud/blob/main/final%20Output.PNG)

**Note :** It may take certain time so do not close the qwiklab window wait and copy above 3 ip 
           address and paste in in seprate windows and refresh it till you got the output(**can take more than a minutes**)
           
 **Ctrl+Z** to quit the cloud console in case not working
