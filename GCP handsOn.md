# GCP HandsOn

##Create a bucket using Cloud Shell
>gsutil mb gs://<BUCKET_NAME>

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