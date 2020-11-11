# Basic Services
## GCS (Google Cloud Storage)
* Bucket name, must be __unique__ across Cloud Storage
* Location type: _(cannot change after the bucket has been created)_
  * __Region__ _(europe-west1, us-east1, etc)_
  * __Dual-region__ _(eur4, nam4)_
  * __Multi-region__ _(us, eu, asia)_
* Storage class:
  * __Standard__ _(Good for “hot” data that’s accessed frequently, including websites, streaming videos, and mobile apps)_
  * __Nearline__  _(Low cost. Good for data that can be stored for at least 30 days, including data backup and long-tail multimedia content.)_
  * __Coldline__ _(Very low cost. Good for data that can be stored for at least 90 days, including disaster recovery.)_
  * __Archive__ _(Lowest cost. Good for data that can be stored for at least 365 days, including regulatory archives.)_
Labels: 
Encryption:
  * __Google-managed key__ _(Encrypt object data with encryption keys stored by the Cloud Key Management Service and managed by you.)_
  * __Customer-managed key__ _(Encrypt object data with encryption keys created and managed by you.)_

> Public object url: https://storage.googleapis.com/bucket-name/object-name

### Links Section
- [Make data public](https://cloud.google.com/storage/docs/access-control/making-data-public)
- [Google Cloud Storage](https://cloud.google.com/storage)

## GCS via gsutil in Command Line
* Show Core config
```sh
gcloud config list

[component_manager]
disable_update_check = True
[compute]
gce_metadata_read_timeout_sec = 30
[core]
account = adrian.test.cloud@gmail.com
disable_usage_reporting = True
project = myprojecttest-293016
[metrics]
environment = devshell

Your active configuration is: [cloudshell-4193]
```

* List buckets and list objects
```sh
# List buckets
$ gsutil ls

gs://eu.artifacts.myprojecttest-293016.appspot.com/
gs://myprojecttest-293016.appspot.com/
gs://staging.myprojecttest-293016.appspot.com/

# List bucket objects
$ gsutil ls gs://storage-lab-console/

gs://storage-lab-console/file.mp4
gs://storage-lab-console/file.txt
gs://storage-lab-console/test/

# List bucket objects recursively
$ gsutil ls gs://storage-lab-console/**

gs://storage-lab-console/file.mp4
gs://storage-lab-console/file.txt
gs://storage-lab-console/test/
gs://storage-lab-console/test/testing.yaml
```

* Make bucket
```sh
# Get help
$ gsutil mb --help

NAME
  mb - Make buckets


SYNOPSIS

  gsutil mb [-b (on|off)] [-c <class>] [-l <location>] [-p <proj_id>]
            [--retention <time>] gs://<bucket_name>...
...

# Make bucket
gsutil mb -l northamerica-northeast1 gs://gcp-testing-lab-2
Creating gs://gcp-testing-lab-2/...
```

* Labels
```sh
# Get labels
$ gsutil label get gs://storage-lab-cli-2
{
  "extralabel": "exgtravalue",
  "function": "learning"
}

# Set Labels in command-line from file
$ gsutil label set bucketsLabels.json gs://gcp-testing-lab-2
Setting label configuration on gs://gcp-testing-lab-2/...

$ gsutil label get gs://gcp-testing-lab-2
{
  "extralabel": "exgtravalue",
  "function": "learning"
}

# Set label in command-live form arg
$ gsutil label ch -l "demolable:demolabelvalue" gs://gcp-testing-lab-2
Setting label configuration on gs://gcp-testing-lab-2/...

$ gsutil label get gs://gcp-testing-lab-2
{
  "demolable": "demolabelvalue",
  "extralabel": "exgtravalue",
  "function": "learning"
}
```

* Versioning
```sh
# Getting versioning status
$ gsutil versioning get gs://storage-lab-cli-2/
gs://gcp-testing-lab-2: Suspended

# Setting versioning ON
$ gsutil versioning set on gs://storage-lab-cli-2/
Enabling versioning for gs://gcp-testing-lab-2/...

# Getting versioning status
$ gsutil versioning get gs://storage-lab-cli-2/
gs://gcp-testing-lab-2: Enabled
```

* Manage objects
```sh
# Copy files
gsutil cp README-cloudshell.txt gs://storage-lab-cli-2/

# List files
gsutil ls gs://storage-lab-cli-2/
gsutil ls -a gs://storage-lab-cli-2/

# Delete files
gsutil rm gs://storage-lab-cli/README-cloudshell.txt

# Permission files
gsutil acl ch -u AllUsers:R gs://storage-lab-cli-2/Selfie.jpg
```

### Links Section
- [Buckets Locations](https://cloud.google.com/storage/docs/locations)

## GCE VM (Google Compute Engine Setup)
* Get config values
```sh
$ gcloud config get-value project
Your active configuration is: [cloudshell-4193]
myprojecttest-293016
```
* Sintaxis
```sh
$ gcloud services -h
Usage: gcloud services [optional flags] <group | command>
  group may be           operations | peered-dns-domains | vpc-peerings
  command may be         disable | enable | list

For detailed information on this command and its flags, run:
  gcloud services --help
```

* List VM
```sh
$ gcloud compute instances list
Listed 0 items.
```

* Show service list
```sh
# Show services list
gcloud services list
NAME                              TITLE
bigquery.googleapis.com           BigQuery API
bigquerystorage.googleapis.com    BigQuery Storage API
cloudapis.googleapis.com          Google Cloud APIs
cloudbuild.googleapis.com         Cloud Build API
clouddebugger.googleapis.com      Cloud Debugger API
cloudtrace.googleapis.com         Cloud Trace API
compute.googleapis.com            Compute Engine API
container.googleapis.com          Kubernetes Engine API
containerregistry.googleapis.com  Container Registry API
datastore.googleapis.com          Cloud Datastore API
iam.googleapis.com                Identity and Access Management (IAM) API
iamcredentials.googleapis.com     IAM Service Account Credentials API
logging.googleapis.com            Cloud Logging API
monitoring.googleapis.com         Cloud Monitoring API
oslogin.googleapis.com            Cloud OS Login API
pubsub.googleapis.com             Cloud Pub/Sub API
servicemanagement.googleapis.com  Service Management API
serviceusage.googleapis.com       Service Usage API
sql-component.googleapis.com      Cloud SQL
storage-api.googleapis.com        Google Cloud Storage JSON API
storage-component.googleapis.com  Cloud Storage
storage.googleapis.com            Cloud Storage API

# Show enable services list
gcloud services list --enabled
NAME                              TITLE
bigquery.googleapis.com           BigQuery API
bigquerystorage.googleapis.com    BigQuery Storage API
cloudapis.googleapis.com          Google Cloud APIs
cloudbuild.googleapis.com         Cloud Build API
clouddebugger.googleapis.com      Cloud Debugger API
cloudtrace.googleapis.com         Cloud Trace API
compute.googleapis.com            Compute Engine API
container.googleapis.com          Kubernetes Engine API
containerregistry.googleapis.com  Container Registry API
datastore.googleapis.com          Cloud Datastore API
iam.googleapis.com                Identity and Access Management (IAM) API
iamcredentials.googleapis.com     IAM Service Account Credentials API
logging.googleapis.com            Cloud Logging API
monitoring.googleapis.com         Cloud Monitoring API
oslogin.googleapis.com            Cloud OS Login API
pubsub.googleapis.com             Cloud Pub/Sub API
servicemanagement.googleapis.com  Service Management API
serviceusage.googleapis.com       Service Usage API
sql-component.googleapis.com      Cloud SQL
storage-api.googleapis.com        Google Cloud Storage JSON API
storage-component.googleapis.com  Cloud Storage
storage.googleapis.com            Cloud Storage API

# Show available services list
$ gcloud services list --available
abusiveexperiencereport.googleapis.com                Abusive Experience Report API
acceleratedmobilepageurl.googleapis.com               Accelerated Mobile Pages (AMP) URL API
accessapproval.googleapis.com                         Access Approval API
accesscontextmanager.googleapis.com                   Access Context Manager API
actions.googleapis.com                                Actions API
adexchangebuyer-json.googleapis.com                   Ad Exchange Buyer API
adexchangebuyer.googleapis.com                        Ad Exchange Buyer API II

...
# Show available services filter list
$ gcloud services list --available | grep compute
compute.googleapis.com                                Compute Engine API
computescanning.googleapis.com                        Compute Scanning API
```

* Managed VM
```sh
# Create VM
$ gcloud compute instances create myvm
Did you mean zone [europe-west1-c] for instance: [myvm] (Y/n)?  Y

Created [https://www.googleapis.com/compute/v1/projects/myprojecttest-293016/zones/europe-west1-c/instances/myvm].
NAME  ZONE            MACHINE_TYPE   PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP    STATUS
myvm  europe-west1-c  n1-standard-1               10.132.0.2   35.205.59.211  RUNNING

# Delete VM
$ gcloud compute instances delete myvm
Did you mean zone [europe-west1-c] for instance: [myvm] (Y/n)?  Y

The following instances will be deleted. Any attached disks configured
 to be auto-deleted will be deleted unless they are attached to any
other instances or the `--keep-disks` flag is given and specifies them
 for keeping. Deleting a disk is irreversible and any data on the disk
 will be lost.
 - [myvm] in [europe-west1-c]

Do you want to continue (Y/n)?  Y

Deleted [https://www.googleapis.com/compute/v1/projects/myprojecttest-293016/zones/europe-west1-c/instances/myvm].
```

## Rundown on gcloud
### Overview
* Command-line tool to interact with GCP
* Best friends with __gsutil__ _(Google Compute Storage)_ and __bq__ _(BigQuery)_
  * All share same configuration set via __gcloud config__
  * __gsutil__ could have been gcloud storage
  * __bq__ could have been gcloud bigquery
* In general: more poweful than console but less powerfull than REST API
* Alpha y Beta versions avialbel via __gcloud alpha__ and __gcloud beta__
  * `gcloud beta billing account list`
  * `gcloud beta billing projects link my-project --billing-account XXX-XXX-XXX`

### Basic Syntax
```sh
gcloud <global flags> <service/product> <group/area> <command> <flags> <parameters>
```
* Always drills down (from left to right)
* Examples
  * `gcloud --project myprojectid compute instances list`
  * `gcloud --project=myprojectid compute instances list`
  * `gcloud compute instances create myvm`
  * `gsutil ls`
  * `gsutil mb -l northamercia-norteast1 gs://storage-name`
  * `gsutil label set bucketlables.json gs://storage-name`

### Global flags
* -- help
* -h
* --project <projectid>
* --account
* --filter 
  * Not always available, but often better than using _grep_
* --format 
  * Can choose _JSON, YAML, CSV, etc_
  * Can pipe ("|") JSON to __jq__ command for futher processing
* --quiet (or _-q_)

### Config properties
* Values entered once and used by any command that needs them
* Can be overridden on a specific command with corresponding flag
* ussed very often for account, project, region, and zone
  * Set "core/account" or "account" to replace _--account_
  * Set "core/project" or "project" to replace _--project_
  * Set "compute/region" to replace "**region"
  * Set "compute/zone" to replace "**zone"
* Set with _gcloud config set <property> <value>_
* Check with _gcloud config set value <property>_
* Clear with _gcloud config unset <property>_

### Configurations
* Can maintain groups of settings and switch between them
* Most useful when using multiple projects
* Iteractive workflow to set common properties in a config with _gcloud init_
* List all properties in a configruation with _gcloud config list_
* List all configurations with _gcloud config configurations list_
  * IS_ACTIVE column shows which one is currently being used
  * Other columns list account, project, region, zone, and the name of the config
* Make new config _gcloud config configurations create ITS-NAME_
* Start ussing config when _gcloud config configurations activate ITS-NAME_
  * Or use for justo one command with _--configuration=ITS-NAME_

### Links section
- [Overview Doc for gcloud](https://cloud.google.com/sdk/gcloud/)
- [Syntax of gcloud](https://cloud.google.com/sdk/gcloud/reference/)
- [Properties of gcloud](https://cloud.google.com/sdk/docs/properties)
- [Configuration in gcloud](https://cloud.google.com/sdk/docs/configurations)

## GCE in and out

```sh
# Look at how to set the machine type
gcloud compute machine-types list
NAME              ZONE                       CPUS  MEMORY_GB    DEPRECATED
e2-highcpu-16     europe-west1-b             16    16.00
e2-highcpu-2      europe-west1-b             2     2.00
e2-highcpu-32     europe-west1-b             32    32.00
e2-highcpu-4      europe-west1-b             4     4.00
e2-highcpu-8      europe-west1-b             8     8.00
e2-highmem-16     europe-west1-b             16    128.00
....

# Show some free*tier*eligible options
gcloud compute machine-types list --filter="NAME:f1-micro"
gcloud compute machine-types list --filter="NAME:f1-micro AND ZONE~us-west"
NAME      ZONE        CPUS  MEMORY_GB  DEPRECATED
f1-micro  us-west1-a  1     0.60
f1-micro  us-west1-b  1     0.60
f1-micro  us-west1-c  1     0.60
f1-micro  us-west2-c  1     0.60
f1-micro  us-west2-b  1     0.60
f1-micro  us-west2-a  1     0.60
f1-micro  us-west3-a  1     0.60
f1-micro  us-west3-b  1     0.60
f1-micro  us-west3-c  1     0.60
f1-micro  us-west4-c  1     0.60
f1-micro  us-west4-a  1     0.60
f1-micro  us-west4-b  1     0.60

# Set our defaults to Los Angeles
gcloud config set compute/zone us-west2-b
gcloud config set compute/region us-west2

# Start our instance
gcloud compute instances create --machine-type=f1-micro myhappyvm
ping -c 3 myhappyvm
ping -c 3 internalipaddress
ping -c 3 externalipaddress

# Connect to the VM
ssh externalipaddress
gcloud compute ssh myhappyvm

# Check out the metadata
curl metadata.google.internal/computeMetadata/v1/
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/project/
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/project/project*id
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/project/attributes/
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/project/attributes/ssh*keys

# Look at some instance metadata
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/instance/
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/instance/name
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/instance/service*accounts/default/
curl *H "Metadata*Flavor: Google" metadata.google.internal/computeMetadata/v1/instance/service*accounts/default/email
```

### Links section
- [Filters in gcloud](https://cloud.google.com/sdk/gcloud/reference/topic/filters)
- [Instace Metadata Reference](https://cloud.google.com/compute/docs/storing-retrieving-metadata)


## GCE via console
### Links section
- [Creating instances](https://cloud.google.com/compute/docs/instances/create-start-instance)
- [Preemptible Instaces](https://cloud.google.com/compute/docs/instances/create-start-preemptible-instance)
- [Startup Scripts](https://cloud.google.com/compute/docs/startupscript)
- [Service Accounts and Scopes](https://cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances)

