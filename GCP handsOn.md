# GCP HandsOn

##Move instance to new zone
>gcloud compute instances move

##Create a bucket using Cloud Shell
```sh
>gsutil mb gs://<BUCKET_NAME>
```

##Create a globally unique bucket name and store it in the environment variable YOUR_BUCKET_NAME
>export YOUR_BUCKET_NAME=<Enter your bucket name here>

>Copy the file into one of the buckets you created earlier in the lab. Replace [MY_FILE] with the file you uploaded and [BUCKET_NAME] with one of your bucket names:
>gsutil cp [MY_FILE] gs://[BUCKET_NAME]

To list available regions, execute the following command:
>gcloud compute regions list

Create an environment variable and replace [YOUR_REGION] with the region you selected in the previous step:
>INFRACLASS_REGION=[YOUR_REGION]

Create a subdirectory for materials used in this class:
```sh
mkdir infraclass
```
Create a file called config in the infraclass directory:
```sh
touch infraclass/config
```

Append the value of your Region environment variable to the config file:

echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config

Create a second environment variable for your Project ID, replacing [YOUR_PROJECT_ID] with your Project ID. You can find the project ID on the GCP Console Home page.

INFRACLASS_PROJECT_ID=[YOUR_PROJECT_ID]

Append the value of your Project ID environment variable to the config file:

echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config

Use the source command to set the environment variables, and use the echo command to verify that the project variable was set:

source infraclass/config
echo $INFRACLASS_PROJECT_ID


Modify the bash profile and create persistence
Edit the shell profile with the following command:

nano .profile

Add the following line to the end of the file:

source infraclass/config
***

Cloud Identity and Access Management (IAM)
Overview
Objectives
Task 1: Setup for two users
Task 2: Explore the IAM console
Task 3: Prepare a resource for access testing
Task 4: Remove project access
Task 5: Add storage access
Task 6: Set up the Service Account User
Task 7: Explore the Service Account User role
Task 8: Review
End your lab

1
Service account details
2
Grant this service account access to project (optional)
3
Grant users access to this service account (optional)


To rename the file you copied, run the following command:
mv sample.txt sample2.txt

To copy the renamed file back to the bucket, run the following command:
gsutil cp sample2.txt gs://[YOUR_BUCKET_NAME]

What happened?

Because you connected via SSH to the instance, you can "act as the service account," essentially assuming the same permissions.The service account the instance was started with had the Storage Viewer role, which permits downloading objects from GCS buckets in the project.To list instances in a project, you need to grant the compute.instance.list permission. Because the service account did not have this permission, you could not list instances running in the project. Because the service account did have permission to download objects, it could download an object from the bucket. It did not have permission to write objects, so you got a "403 access denied" message.


What abstraction is primarily used to administer user access in Cloud IAM ?
Roles, an abstraction of job roles.

How is a user identity created in Cloud IAM?
User identities are created from outside of GCP in a Google-administered domain.

What technology can be used along with Cloud IAM to provide another layer of security and access control in GCP?
Networking; specifically firewall rules.



Cloud Storage
Overview
Cloud Storage is a fundamental resource in GCP, with many advanced features. In this lab, you exercise many Cloud Storage features that could be useful in your designs. You explore Cloud Storage using both the console and the gsutil tool.


Overview
Objectives
Task 1: Preparation
Task 2: Access control lists (ACLs)
Task 3: Customer-supplied encryption keys (CSEK)
Task 4: Rotate CSEK keys
Task 5: Enable lifecycle management
Task 6: Enable versioning
Task 7: Synchronize a directory to a bucket
Task 8: Cross-project sharing
Task 9: Review
End your lab

IP Addresses: https://cloud.google.com/compute/docs/ip-addresses/

Subnets and CIDR ranges: https://cloud.google.com/compute/docs/alias-ip/#subnets_and_cidr_ranges

Reflecting the new tighter policies, the new subnetwork is CIDR /26. How many VMs can that support?/26 = 64 addresses, minus broadcast, subnet, and gateway = 61 VMs.


Big query select , [DatasetID.TableID.Field]

To verify that gcloud is configured to [PROJECT_ID], run the following command:
gcloud config list project

In Cloud Shell, to create the vpn-1 gateway, run the following command:
gcloud compute target-vpn-gateways \
create vpn-1 \
--network vpn-network-1  \
--region us-east1

To reserve a Static IP for the vpn-1 gateway, run the following command:
gcloud compute addresses create --region us-east1 vpn-1-static-ip

To view the Static IP for the vpn-1 gateway, run the following command:
gcloud compute addresses list

To store the Static IP for the vpn-1 gateway, in an environment variable, run the following command, and replace the IP address with the address from the output of the last command:
export STATIC_IP_VPN_1=<Enter IP address for vpn-1 here>

To create ESP forwarding for vpn-1, run the following command:
gcloud compute \
forwarding-rules create vpn-1-esp \
--region us-east1  \
--ip-protocol ESP  \
--address $STATIC_IP_VPN_1 \
--target-vpn-gateway vpn-1

To create UDP500 forwarding for vpn-1, run the following command:
gcloud compute \
forwarding-rules create vpn-1-udp500  \
--region us-east1 \
--ip-protocol UDP \
--ports 500 \
--address $STATIC_IP_VPN_1 \
--target-vpn-gateway vpn-1

In the GCP Console, on the Navigation menu ( 7a91d354499ac9f1.png), click VPC network > External IP addresses.
Verify that both regions have an external IP address reserved and that all three forwarding rules are displayed in the__ In use by__ column.
Alternatively, you can reserve static addresses and set forwarding rules through this section of the GCP Console.

In Cloud Shell, to verify the VPN gateways, run the following command:
gcloud compute target-vpn-gateways list

To create the tunnel for traffic from Network-1 to Network-2, run the following command:
gcloud compute \
vpn-tunnels create tunnel1to2  \
--peer-address $STATIC_IP_VPN_2 \
--region us-east1 \
--ike-version 2 \
--shared-secret gcprocks \
--target-vpn-gateway vpn-1 \
--local-traffic-selector 0.0.0.0/0 \
--remote-traffic-selector 0.0.0.0/0

To create a static route from Network-1 to Network-2, run the following command:
gcloud compute  \
routes create route1to2  \
--network vpn-network-1 \
--next-hop-vpn-tunnel tunnel1to2 \
--next-hop-vpn-tunnel-region us-east1 \
--destination-range 10.1.3.0/24


## Virtual Machine Automation and Load Balancing v1.5
### Configure the external load balancer

Choose a region and zone from the list of available regions and zones
```sh
gcloud compute regions list
gcloud compute zones list
```

create environments for your selected region and zones
```sh
export MY_REGION=<Enter YOUR_REGION here>
export MY_ZONE1=<Enter YOUR_ZONE1 here>
export MY_ZONE2=<Enter YOUR_ZONE2 here>
```

target pool is named extloadbalancer and is connected to the health check you created in the previous step
```sh
gcloud compute target-pools create extloadbalancer \
    --region $MY_REGION --http-health-check webserver-health
```

Add the three VMs, webserver1, webserver2, and webserver3, into the target pool extloadbalancer.
```sh
gcloud compute target-pools add-instances extloadbalancer \
    --instances webserver1,webserver2,webserver3 \
     --instances-zone=$MY_ZONE1
```

### Create the forwarding rule
get the reserved static IP address , and create an environment variable for the static external IP
```sh
gcloud compute addresses list
export STATIC_EXTERNAL_IP=[YOUR_STATIC_IP]
```

complete the configuration of the forwarding rule
```sh
gcloud compute forwarding-rules create webserver-rule \
    --region $MY_REGION --ports 80 \
    --address $STATIC_EXTERNAL_IP --target-pool extloadbalancer
```

Launch two new servers in the second zone
```sh
gcloud compute instances create webserver4 \
    --image-family debian-9 \
    --image-project debian-cloud \
    --tags int-lb \
    --zone $MY_ZONE2 \
    --subnet default \
    --metadata startup-script-url="gs://cloud-training/archinfra/mystartupscript",my-server-id="WebServer-4"
```

Create an instance group for each zone and add the instances
create ig1 in your first zone
```sh
gcloud compute instance-groups unmanaged create ig1 \
    --zone $MY_ZONE1
```

add webserver2 and webserver3 to ig1
```sh
gcloud compute instance-groups unmanaged add-instances ig1 \
    --instances=webserver2,webserver3 --zone $MY_ZONE1
```

### Configure the load balancer

create a health check
```sh
gcloud compute health-checks create tcp my-tcp-health-check \
    --port 80
```

create a backend service
```sh
gcloud compute backend-services create my-int-lb \
    --load-balancing-scheme internal \
    --region $MY_REGION \
    --health-checks my-tcp-health-check \
    --protocol tcp
```

add ig1 to your backend service
```sh
gcloud compute backend-services add-backend my-int-lb \
    --instance-group ig1 \
    --instance-group-zone $MY_ZONE1 \
    --region $MY_REGION
```

configure a firewall rule to allow traffic to the load balancer and from the load balancer to the instances
```sh
gcloud compute firewall-rules create allow-internal-lb \
    --network default \
    --source-ranges 0.0.0.0/0 \
    --target-tags int-lb \
    --allow tcp:80,tcp:443
```

configure another firewall rule to allow health check probes from the health checker
```sh
gcloud compute firewall-rules create allow-health-check \
    --network default \
    --source-ranges 130.211.0.0/22,35.191.0.0/16 \
    --target-tags int-lb \
    --allow tcp
```

### Create a standalone client
create the client
```sh
gcloud compute instances create standalone-instance-1 \
    --image-family debian-9 \
    --image-project debian-cloud \
    --zone $MY_ZONE1 \
    --tags standalone \
    --subnet default
```

create a firewall rule to allow SSH connections to the standalone client instance
```sh
gcloud compute firewall-rules create allow-ssh-to-standalone \
    --network default \
    --target-tags standalone \
    --allow tcp:22
```


#### How does the autoscaler resolve conflicts between multiple scaling policies?
1. First come, first served.
2. It selects the one that recommends the most VMs, to ensure the application is supported.
3. It selects the one with the fewest VMs to provide the lowest cost.
4. It is based on priority, a value set in each policy that determines the precedence.


#### The following command enables autoscaling for a managed instance group using CPU Utilization:
Which of the following statements correctly explains what the command is creating?
1. The command creates an autoscaler that has a target CPU utilization of 75% with a maximum of 20 VMs that will shut down a VM 90 seconds after the request.
2. The command creates an autoscaler that has a target CPU utilization of 75% with a maximum of 20 VMs that will start collecting information about a VM 90 seconds after it is created.
3. The command creates an autoscaler that has a target CPU utilization of 75% with a maximum of 60 VMs that will shut down 90 seconds after the request.
4. All options are correct.


#### Which statement is true of autoscaling custom metrics.
1. Autoscaling does not support custom metrics.
2. Custom metrics are much slower than native autoscaling metrics, so avoid using them.
3. Stackdriver metrics can be used as custom metrics for autoscaling policies.
4. Every custom metric includes a multiplier variable that you can use to adjust the input value range.

## Autoscaling v1.5
### Configure the external load balancer

Choose a region and zone from the list of available regions and zones
```sh
gcloud compute regions list
gcloud compute zones list
```

## Google Cloud Platform API Infrastructure Automation v1.5
### Authorize the VM to use the Cloud SDK
check whether the SDK is installed on this VM
```sh
gcloud -v
```

To see whether the permissions are set to make calls to Google Cloud
```sh
gcloud compute zones list
```

To authorize the VM with the credentials you just uploaded
```sh
gcloud auth activate-service-account --key-file credentials.json
```

Verify the Hadoop cluster
SSH into the Hadoop Master VM
```sh
gcloud compute ssh --zone=us-east1-b $UNIQUE_ID-m
```

To create a Hadoop file system directory
```sh
hadoop fs -mkdir testsetup
```


#### What is a fundamental difference between a snapshot of a boot persistent disk and a custom image?
1. A snapshot is only for backing up data and cannot be used to create a VM.
2. A snapshot is locked within a project, but a custom image can be shared between projects.
3. A custom image can only be used in disaster recovery.
4. There is no difference, they are different names for the same thing.


#### What happens when a custom images is marked "Obsolete" ?
1. No new projects can use the custom image, but those already with the image can continue to use it.
2. All VMs based on the custom image immediately terminate.
3. VMs that are based on the custom image continue to run, but cannot be re-launched.
4. A warning is displayed to new users that the image is no longer supported and will not be maintained or fixed.


#### From where can you import boot disk images for Compute Engine (select 3)?
1. Virtual machines on your local workstation
2. Your physical datacenter
3. Google Flash, an online boot disk image storage
4. Virtual machines that run on another cloud platform


#### What kinds of files form the Deployment Manager templates?
1. Templates are composed of yaml, java, and Node.js files.
2. Templates are composed of yaml, python, and jinja2 files.
3。 Templates are composed of Powershell, python, and text files.
4. Templates are composed of bash, yaml, and Angular.js files.

#### What service does Cloud Launcher provide?
1. Provides pre-packaged 3rd party solutions using Deployment Manager templates.
2. It is an Android app that sends notifications when new Zones are launched.
3. Provides 3rd party solutions using the Google Cloud API and bash scripts.
4. Provides an open source standard alternative to Deployment Manager.


#### Which of the following is true of Deployment Manager Templates?
1. They cannot be nested, can use environment variables, but do not have their own properties.
2. They can be nested, but cannot share data except as passed in an external file.
3. There can be multiple templates, but they cannot be nested and don't share properties or variables.
4. They can be nested, have properties, and can use environment variables.

#### How are Managed Services useful?
1. Managed Services are more customizable than infrastructure solutions.
2. Managed Services may be an alternative to creating and managing infrastructure solutions.
3. If you have an existing infrastructure service, Google will manage it for you if you purchase a Managed Services contract.
4. Managed Services are pay services offered by 3rd party vendors.

#### Which of the following are data processing Managed Services?
1. Dataproc, Datastudio, and Google Cloud Storage.
2. Google Compute Engine, Cloud IAM, and Hadoop.
3. Dataproc, Dataflow, and BigQuery.
4. Google Hadoop Manager, DataQuery, BigProc

#### Which of the following is a feature of Dataproc?
1. It typically takes less than 90 seconds to start a cluster.
2. Dataproc allows full control over HDFS advanced settings.
3. Dataproc billing occurs in 10-hour intervals.
4. It doesn't integrate with Stackdriver, but it has its own monitoring system.


## Introducing Google Cloud Platform

#### Choose fundamental characteristics of cloud computing. Mark all that are correct (4 correct responses).
1. All resources are open-source-based
2. Resources are available from anywhere over the network
3. Customers pay only for what they use or reserve
4. Computing resources available on-demand and self-service
5. Customers can scale their resource use up and down
6. Customers are required to commit to multi-year contracts
7. Providers always dedicate physical resources to each customer

#### Choose a fundamental characteristic of devices in a virtualized data center.
1. They are available from anywhere on the Internet.
2. They use less resources than devices in a physical data center.
3. They are more secure.
4. They are manageable separately from the underlying hardware.

#### What type of cloud computing service lets you bind your application code to libraries that give access to the infrastructure your application needs?
1. Platform as a Service
2. Infrastructure as a Service
3. Software as a Service
4. Hybrid cloud
5. Virtualized data centers

#### What type of cloud computing services provide raw compute, storage, and network, organized in ways that are familiar from physical data centers?
1. Infrastructure as a Service
2. Sofware as a Service
3. Platform as a Service
4. Database as a Service

#### Which statement is true about the zones within a region?
1. The zones within a region are never closer to each other than 160 km
2. Customers must choose exactly onde zone in each region to run their resources
3. The zones within a region have fast network connectivity among them
4. Each zone corresponds to a single physical data center

## Deployment Manager v1.5
download files from bucket
```sh
gsutil cp gs://cloud-trainning/archinfra/dm* .
```

unzip the archive
```sh
unzip dm-net-v01.zip
```

### Deploy the configuration
deploy base on the config
```sh
gcloud deployment-manager deployments create gcpinfra --config=net-config.yaml
```

list the type of GCP resouces that you can control using deployment Manager
```sh
gcloud deployment-manager types list
```
