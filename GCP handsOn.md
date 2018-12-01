# GCP HandsOn

##Move instance to new zone
>gcloud compute instances move

##Create a bucket using Cloud Shell
>gsutil mb gs://<BUCKET_NAME>

##Create a globally unique bucket name and store it in the environment variable YOUR_BUCKET_NAME
>export YOUR_BUCKET_NAME=<Enter your bucket name here>

>Copy the file into one of the buckets you created earlier in the lab. Replace [MY_FILE] with the file you uploaded and [BUCKET_NAME] with one of your bucket names:
>gsutil cp [MY_FILE] gs://[BUCKET_NAME]

To list available regions, execute the following command:
>gcloud compute regions list

Create an environment variable and replace [YOUR_REGION] with the region you selected in the previous step:
>INFRACLASS_REGION=[YOUR_REGION]

Create a subdirectory for materials used in this class:

mkdir infraclass

Create a file called config in the infraclass directory:

touch infraclass/config

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
