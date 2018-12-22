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

Reflecting the new tighter policies, the new subnetwork is CIDR /26. How many VMs can that support?/26 = 64 addresses (2 * 30-26 次方
  ), minus broadcast, subnet, and gateway = 61 VMs.


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


## Cloud IAM Study
1. Organization level: The organization resource represents your company.
2. Services within the same project have a default level of trust.
3. Child policies cannot restrict access granted at the parent.
4. When using Cloud IAM, a best practice is to follow the principle of least privilege. The
principle applies to identities, roles, and resources.
5. Primitive roles: The original roles available in the Google Cloud Platform Console. These are the Owner, Editor, and Viewer roles. Still assigned by default to projects. Primitive roles are quite broad.
6. Product-specific roles
eg Compute Engine roles
○ Compute Engine Instance Admin: VMs and disks
○ Service Account User: service accounts
○ Compute Engine Image User: images
○ Compute Engine Network Viewer: read-only for all networking
7. A service account is an identity for your programs to use to authenticate and gain
access to Google Cloud Platform APIs
For example, if you write an application that reads and writes files on Cloud Storage, you need to
○ authenticate to the to either the Google Cloud Storage XML API or JSON
API.
○ program the application to obtain credentials from the service account.
○ Your application authenticates seamlessly to the API without embedding any secret keys or credentials in your instance, image, or application code.
8. Customizing scopes for a VM , Service accounts can use scopes through the Cloud SDK. gcloud and gsutil
9. Cloud IAP (Identity-Aware Proxy) , setup a central authorization layer for application accessed by https. so you can use this application level access instead of network level firewals

#### What abstraction is primarily used to administer user access in Cloud IAM ?
1. Leases, an abstraction of periodic entitlements.
2. Roles, an abstraction of job roles.
3. Credentials, an abstraction of an authorization token.
4. privileges, an abstraction of access rights

#### How is a user identity created in Cloud IAM?
1. User identities are created from the Cloud identity console that is only visible to GCP Super-administrators.
2. User identities are created from the cloud IAM area of the GCP console, or by using the gcloud command.
3. User identities are created through a frderated Active Directiory domain.
4. User identities are created from outside of GCP in a Google-administered domain.

What technology can be used along with Cloud IAM to provide another layer of security and access control in GCP?
1. Machine learning;specifically,intrusion detection.
2. Antivirus and anti-exploit Software built into GCP VMs.
3. Networking; specifically firewall rules.
4. Dynamic per-user resource throttling.


Cloud Identity and Access Management (IAM) HandsOn Lab
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

## Data Storage services
Storage & Database decision
1. Cloud storage: like file system , store blobs in buckets
   regional/muti-regional/nearline/coldline
   Strong global consistency - immediately available after insert/update
2. Cloud SQL: hosted Relational database , No-ops
3. Cloud Spanner: Relational database,Globally/horizontal scalable
4. Cloud datastore: Persistend Hashmap,structured database , key-entry storage system (not key-value)
    schemaless , being able to store any entity.
    sql-like capabilities
    used with app engine, also with memcache.
    kind=table/entity=row/property=field/key=primary key
    free daily quota
    supports ACID transactions
5. Cloud BigTable: Key-values , HBase, put row , NoSQL

#### Create a bucket using Cloud Shell
```sh
>gsutil mb gs://<BUCKET_NAME>
```

#### Rename - gsutil mv
```sh
gsutil mv gs://[BUCKET_NAME]/[OLD_OBJECT_NAME] gs://[BUCKET_NAME]/[NEW_OBJECT_NAME]
```

#### Copy - gsutil cp
```sh
gsutil mv gs://[BUCKET_NAME]/[OLD_OBJECT_NAME] gs://[BUCKET_NAME]/[NEW_OBJECT_NAME]
```

#### Move - gsutil mv
```sh
gsutil mv gs://[SOURCE_BUCKET_NAME]/[SOURCE_OBJECT_NAME] gs://[DESTINATION_BUCKET_NAME]/[DESTINATION_OBJECT_NAME]
```

#### Check/Modify ACL - gsutil acl get/set
```sh
gsutil acl get gs://bucket/file.txt > acl.txt
gsutil acl set acl.txt gs://bucket/*.jpg
```

#### Detail ACL grant to user(-u)/group(-g)/Project(-p) with read/write/Owner authority
```sh
gsutil acl ch -u john.doe@example.com:W gs://ryan4299899bbb
```

#### lifecycle - Get or set lifecycle configuration for a bucket
```sh
gsutil lifecycle get gs://ryan4299899bbb
gsutil lifecycle set [config-json-file] url...
```

#### versioning
```sh
gsutil versioning get gs:/ryan4299899
gsutil versioning set [on|off] gs://ryan4299899bbb
```

#### rsync - Synchronize content of two buckets/directories
```sh
gsutil rsync [OPTION]... src_url dst_url
gsutil rsync -d data gs://mybucket/data  - to make gs://mybucket/data match the contents of the local directory "data"
gsutil rsync -r data gs://mybucket/data  -  To copy only new/changed files without deleting extra files from gs://mybucket/data leave off the -d option:
gsutil -m rsync -d -r data gs://mybucket/data  -m option, to perform parallel (multi-threaded/multi-processing) synchronization:
```

#### You are developing an application that transcodes large video files. Which storage option is the best choice for your application?
Because video files are blobs and cloud storage is cheap, I would use Google Cloud Storage for this application.

#### You manufacture devices with sensors and need to stream huge amounts of data from those devices to a storage option in the cloud. Which Google Cloud Platform storage option is the best choice for your application?
The key to this question is, streaming huge amounts of data. When you are accumulating lots of data quickly, Bigtable is ideal.

#### Compare labels and tags ?
Labels are a way to organize resources across GCP , user-defined strings in key-value information
Tags are apply to instance only , primarily used for networking

## Virtual-Networks

CIDR主要是一个按位的、基于前缀的，用于解释IP地址的标准。它通过把多个地址块组合到一个路由表表项而使得路由更加方便。这些地址块叫做CIDR地址块。当用二进制表示这些地址时，它们有着在开头部分的一系列相同的位。IPv4的CIDR地址块的表示方法和IPv4地址的表示方法是相似的：由四部分组成的点分十进制地址，后跟一个斜线，最后是范围在0到32之间的一个数字：A.B.C.D/N。点分十进制的部分和IPv4地址一样是一个被分成四个八位位组的32位二进制数。斜线后面的数字就是前缀长度，也就是从左到右，被地址块里的地址所共享的位的数目。当只需说明大概时，十进制部分有时会被省略，因此，/20就表示一个前缀长度是20的CIDR地址块。如果一个IP地址的前N位与一个CIDR地址块的前缀是相同的话，那么就说这个地址属于这个CIDR地址块，也可以说是与CIDR地址块的前缀匹配。所以，要理解CIDR，就要把地址写成二进制的形式。因为IPv4地址的长度总是32位，N位长的CIDR前缀就意味着地址里 {\displaystyle 32-N} 32-N位不匹配。这些位有 {\displaystyle 2^{(32-N)}} 2^{{(32-N)}}种不同的组合，即 {\displaystyle 2^{(32-N)}} 2^{{(32-N)}}个IPv4地址与CIDR地址块的前缀匹配。前缀越短就能匹配越多的地址，越长就匹配得越少。一个地址可能与多个长度不同的CIDR前缀匹配。

#### DNS resolution
1. Internal: 实例的内部完全限定域名 (FQDN) 采用以下格式 [HOST_NAME].c.[PROJECT_ID].internal
2. External: User can directly connect using external ip , or publish public DNS (outside of GCP) , DNS zones can be host using Cloud DNS
3. Cloud DNS: Publish your domain names using Google's infrastructure for production-quality, high-volume DNS services. Google's global network of anycast name servers provide reliable, low-latency authoritative name lookups for your domains from anywhere in the world.

### VPC 特性
1. 全球性. 单个 Google Cloud VPC 可以横跨多个区域，而无需在公共互联网上进行通信。通过 VPC 与本地资源之间的单个连接点即可在全球访问 VPC，降低了成本和复杂性
![VPC全球性](https://cloud.google.com/images/products/virtual-network/global.svg "VPC全球性")

3. 可扩展. Google Cloud VPC 让您无需关闭任何工作负载或停机就能增加任意子网的 IP 空间。这为您提供了灵活性和增长选项，从而满足您的需求。
![VPC可扩展](https://cloud.google.com/images/products/virtual-network/expandable.gif "VPC可扩展")

#### Alias IP ranges
1. 所有子网都具有“主要 CIDR 范围”，也就是用于定义子网的内部 IP 地址范围。每个虚拟机实例均从该范围内获取其主要内部 IP 地址。您还可以从该主要范围分配别名 IP 范围，或者向子网添加次要范围，并从次要范围分配别名 IP 范围。使用别名 IP 范围时，次要子网范围并非必需。这些次要子网范围仅用于提供一种组织工具。
2. 配置了别名 IP 范围时，GCP 将自动安装 VPC 网络路由，以便为主要网络接口的子网获得主要和别名 IP 范围。这可以简化路由流量并管理您的容器。
3. 别名 IP 地址可以通过 Cloud Router 发布到通过 VPN 或互连连接的本地部署网络。
4. 从次要 CIDR 范围分配别名 IP 范围具有一定的优势。由于分配时所使用的范围与主要 IP 地址所使用的范围彼此分离，因此您可以将基础架构（虚拟机）与服务（容器）分离开来。在为基础架构和服务配置不同的地址空间时，可以独立于虚拟机主要 IP 地址的防火墙控制，为虚拟机别名 IP 地址另行设置防火墙控制。例如，您可以允许针对某些容器 pod 的流量，并拒绝针对虚拟机主要 IP 地址的类似流量。

##### 示例：配置使用别名 IP 范围的容器
![alias-ip](https://cloud.google.com/vpc/images/alias-ip/alias-ip-2.svg "alias-ip")

要创建上图所示配置，请执行以下操作：

1. 创建一个子网，使用 CIDR 范围 10.128.0.0/16（从此范围内分配虚拟机 IP 地址），并使用仅供容器使用的次要 CIDR 范围 172.16.0.0/20，此次要范围会配置为托管它们的虚拟机内的别名 IP 范围：
```sh
gcloud compute networks subnets create subnet-a \
    --network network-a \
    --range 10.128.0.0/16 \
    --secondary-range container-range=172.16.0.0/20
```
2. 创建虚拟机，使用范围 10.128.0.0/16 内的主要 IP 地址和次要 CIDR 范围 172.16.0.0/20 内的别名 IP 范围 172.16.0.0/24，供虚拟机内的容器使用：
```sh
gcloud compute instances create vm1 [...] \
    --network-interface subnet=subnet-a,aliases=container-range:172.16.0.0/24
gcloud compute instances create vm2 [...] \
    --network-interface subnet=subnet-a,aliases=container-range:172.16.1.0/24
```

容器 IP 地址在 GCP 中配置为别名 IP 地址。在此设置中，主要和别名 IP 均可通过 VPN 隧道访问。如果配置了 Cloud Router，则它会自动通告次要子网范围 172.16.0.0/20。要详细了解如何将 VPN 与 Cloud Router 搭配使用，请参阅使用动态路由创建 VPN 隧道。

##### 示例：在单个虚拟机实例中配置多个别名 IP 范围
```sh
1. create network
gcloud compute networks create vpc1 --subnet-mode custom

2. create subnet
gcloud compute networks subnets create subnet1 --region us-central1 --network vpc1 --range 10.128.0.0/16 --secondary-range secondaryrange1=172.16.0.0/20

3. create vm bind to the subnet1
gcloud compute instances create vm1 --zone us-central1-a --network-interface "subnet=subnet1,aliases=secondaryrange1:172.16.0.0/27;secondaryrange1:172.16.1.0/32"
```

subnet参数若有被双引号围起来，则为在主要 CIDR 范围内创建具有别名 IP 范围的虚拟机； 若无双引号则为在次要 CIDR 范围内创建具有别名 IP 范围的虚拟机

##### delete network
1. all Vm & firewall rules must be deleted First
2. subnetwork can not be deleted on auto-mode network(can delete under custom netwotrks)
3. On auto-mode network , only the entire network can be deleted


#####  Explore connectivity

| Subnet  | location | Range |
| ------ | ------ | ------ |
| subnet-1a | us-east1 | 192.168.5.0/24 |
| subnet-1b | us-east1 | 192.168.3.0/24 |
| subnet-2 | us-west1 | 192.168.7.0/24 |

| VM  | Network | Subnet  | Region | Zone |
| ------ | ------ | ------ |
| learn-1 | default | n/a | us-east1 | us-east1-b |
| learn-2 | learnauto | n/a | us-east1 | us-east1-b |
| learn-3 | learncustom | subnet-1a | us-east1 | us-east1-b |
| learn-4 | learncustom | subnet-1a | us-east1 | us-east1-c |
| learn-5 | learncustom | subnet-2 | us-west1 | us-west1-a |

1. firewall rules will not auto create for custom networks , it'll create for default/auto networks.
2. routes will create for all 3 network types

Step 1 ping from learn-1
Console: Products and Services > Compute Engine > VM instances , Click on the link to SSH to learn-1.

```sh
$ ping learn-1 , This should succeed.
$ ping learn-2 , Name or service not known , It is because DNS is scoped to network. The VM learn-2 is not in the default network where learn-1 is located.
$ ping <learn-2 external IP> , This should succeed. learn-2 is in an auto-type network, so firewall rules were automatically created that enabled ingress traffic to reach its external IP.
$ ping <learn-3 external IP> , this should failed , learn-3 is in a custom-type network, and no firewall rules were established. You need to creat a firewall rule to permit access.
```

Step 2 ping from learn-3
```sh
$ ping learn-4 , ping learn-5 , DNS translation is working , however no package is deliverd to target VM
PING learn5.c.qwiklabs-gcp-1c1e9db7bdb37581.internal (192.168.7.2) 56(84) bytes of data.
DNS translation is working both learn-4 and learn-5 because all of these VMs are in the same network as learn-4, the learncustom network.
But package not sent to target as we have firewall rules to allow tag only.
```

Increase the address range
```sh
$ gcloud compute networks subnets \
expand-ip-range new-useast  \
--prefix-length 24 \
--region us-east1
```

#####  Common Network designs
1. Routes & firewalls are global resource.
2. Subnets can't span regions.
3. Availablity , 1 project/1 network/1 region/1 subnetwork/deploy vm to multiple zones
4. Globalization , 1 project/1 network/multiple region/2 subnetworks/deploy vm to multiple zones , because VMs are in the single network , they can talk trough GCP's internal global network even they're different zones
5. Cross-project VPC network peering  , multiple project/multiple network/multiple region/multiple zones/multiple subnetworks, Using Sharing mechannism enables collaboration between parts , while isolation prevents error spread to other parts
6. Management seperation , multiple project/multiple network/1 region/1 zones/multiple subnetworks, seperate projects means fine-grained control. But network can not cross projects , so they need to talk to each other via internet istead of GCP internal network.
7. Bastion hosts ,
8. NAT gateway host isolation (将实例配置为 NAT 网关)

#### Lab: Bastion Host
1. Create webserver VM which you wanna protect , have a "webserver" service
2. Restrict firewall rule settings for HTTP : select the default-allow-http rule , in Source filter, change this to IP ranges , and range mark to your IP address
3. Restrict access to the VM from the Internet - Remove the External IP - change it from Ephemeral to none.
4. Create bastion VM , you can directly ping & curl "webserver" since they're in the same network , they can communicate over internal ip
You restricted access to the webserver VM by removing it's external IP address
You created a bastion host named bastion to gain access to the webserver VM over it's internal IP.
Normally, you would harden the bastion host by restricting the source IPs that can access the bastion host, by editing the firewall rules just as you did earlier in this lab.

What address is reserved for the router address? - 10.0.0.1
What address is reserved for the broadcast address? - 10.0.0.255
How many IP addresses are assigned by default to a VM after creation? - 2, an internal IP and an external IP

## Virtual Michines
1. Inferred instances discount : Usage of the same Michine type in the same zone is combined like they're 1 Michine, to give u best discount.
2. Linux-SSH,need firewall allow tcp:22, Windows:RDP,need firewall allow tcp:3389
3. Instance reset: keep ip address,disk,etc , but all data will will clean.
   instance restart: keep most of the things
   instance delete then create : it may have diff ip address , physical hardware , etc
```sh
gcloud compute instances reset example-instance
gcloud compute instances start example-instance
gcloud compute instances describe <instance> - check instance status
```

#### Lab: Creating a Virtual Machine
```sh
gcloud compute instances create gcelab2 --zone us-central1-c
gcloud config set compute/zone - set default zone
```

#### Lab: Work with virtual machines
##### Create the VM Instance
1. Add API access for Cloud Storage
2. Create an additional data disk , will store in cloud storage
3. Add a Tag for a firewall rule
4. Create an External static IP

##### Prepare the data disk
1. Create a directory
```sh
sudo mkdir -p /home/minecraft
```
2. Format the disk
```sh
sudo mkfs.ext4 -F -E lazy_itable_init=0,\
lazy_journal_init=0,discard \
/dev/disk/by-id/google-minecraft-disk
```
3. Mount the disk
```sh
sudo mount -o discard,defaults /dev/disk/by-id/google-minecraft-disk /home/minecraft
```

##### Install and run the application
##### Allow client traffic - setup firewall rules to allow specific tag on tcp:25565
##### Schedule regular backups
```sh
gsutil mb gs://ryan4299899CCCbackup - create bucket
sudo nano /home/minecraft/backup.sh - Create a backup script
sudo chmod 755 /home/minecraft/backup.sh - Make the script executable
sudo crontab -e -- Open the cron table for editing:
0 */4 * * * /home/minecraft/backup.sh - this will create about 300 backups a month in Cloud Storage
Edit VM properties , Custom metadata , to add start-up/shutdown script

Start-up
#!/bin/bash
mount /dev/disk/by-id/google-minecraft-disk /home/minecraft
(crontab -l ; echo "0 */4 * * * /home/minecraft/backup.sh")| crontab -
cd /home/minecraft
screen -d -m -S mcs java -Xms1G -Xmx7G -d64 -jar minecraft_server.1.11.2.jar nogui

shut-down
#!/bin/bash
sudo screen -r -X stuff '/stop\n'
```

These scripts will run automatically when you start or stop your instance.
When you restart your instance, the startup-script will automatically mount the Minecraft disk to the appropriate directory, reinstall your cron job, start your Minecraft server in a screen session, and detach the session.
When you stop the instance, the shutdown-script will shut down your Minecraft server before the instance shuts down.

## Container and Services 01 - Application infrastructure service
### Cloud Pub/Sub
#### The Basic
1. Publisher publish a message to Topic
2. Topic store messages for Availablity & reliability
3. Topic sent message to Subscription(订阅)
4. Subscription determine which Subscriber to receive message & sent
5. After message consumed , Subscriber sent back acknowledgement back to Subscription
6. Subscription removed the mesage when all deliveries are complete.
> 在此方案中，有两个发布者在单个主题上发布消息。该主题有两个订阅，第一个订阅有两个订阅者，第二个订阅有一个订阅者。粗体字母代表消息。消息 A 来自发布者 1，通过订阅 1 发送给订阅者 2，通过订阅 2 发送给订阅者 3。消息 B 来自发布者 2，通过订阅 1 发送给订阅者 1，通过订阅 2 发送给订阅者 3。

![Pub/Sub basic](https://cloud.google.com/pubsub/images/wp_flow.svg "Pub/Sub basic")

### Cloud Endpoints - API management
### Cloud Function - = AWS LAMDA
### Cloud Source Repositories
### Cloud Machine learning

## Container and Services 02 - Application development service
### App engine (GAE) is a PaaS
#### Comparing env (Standard vs Flexible)

| Feature  | Standard | Flexible |
| ------ | ------ | ------ |
| Instance start up | in mill sec | in minutes|
| SSH Debug | No | Yes |
| Install 3rd binaries | No | Yes |
| Language Support | limited | Any |

## Container and Services 03 - Containers
