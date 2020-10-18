# gcp-certified-associate

6. Account Setup
# Billing Export
- Export must be set up per billing account
- Resoureces should be placed into appropiate projects
- Resources should be ttagged with labels
- Billing export is not real-time
  - Delay is hours

https://cloud.google.com/billing/docs/how-to/export-data-bigquery

# Billing IAM
Role: billing account user
Purpose: Link projects to billing account.
Level: organizciotn or billing account.
Use Case: this role has very restricted permissions, so you can grant it broadly, typically in combination with Project Creator.
These two roles allow a user to create new projects linked to the billing account on which the role is granted.

Get email address of non-admin Google account you control
- not the admin account we created when signing up for GCP
- This will be our "user" account
- Cloud be pre-existing Google account
- Could make Google account for any existing email address
- Could make new Gmail account

Links:
- https://cloud.google.com/billing/docs/how-to/billing-access


7. Cloud Shell and Data Flows

# Explore Cloud Shell 
> Google Cloud Shel provides you with command-line access to your cloud resources directly from your browser.
> You can easily manage your projects and resources without having to install the Google Cloud SDK or other tools on your system.
> With Cloud Shell, the Cloud SDK gcloud command-line tool and other utilities you need are always available, up to date and fully authenticated when you need them.

## Highlights
- Web browser access
  - No need for local terminal
    - Chromebook
    - No PuTTY
  - Automatic SSH key management
- 5 GB of persistent storage
- Easy-access to preinstalled tools
  - gcloud, bq, kubectl, docker, bash, python, etc
- Pre-authorized an always up-to-date
- Web preview of web app running on local port

Links:
- https://cloud.google.com/shell/
- https://github.com/ACloudGuru/gcp-cloud-engineer

# Data Flows
## Mental Models
A simplified representation of reality, which is...
Used by your mind to anticipate events or draw conclusions
Systems combine
- Build large systems out of smaller ones (abstractions)
- Aooming in and out
- 
## Key Takeaways
Data flows are the foundation of every system
Moving, Processing, Remembering
- Not _just_ Network, Compute, Storage
Build mental models
- Helps you make predictions
Identify and think through data flows
- Highlights potential issues
Requierements and options not always clear
- Especially in the real world
Critial skill for both real world and exam questions.


8. Basic Services
# Google Cloud Storage
- Bucket name, must be unique across Cloud Storage
- Location type:  (cannot change after the bucket has been created)
  - Region (europe-west1, us-east1, etc)
  - Dual-region (eur4, nam4)
  - Multi-region (us, eu, asia)
- Storage class:
  - Standard
  - Nearline
  - Coldline
  - Archive
Labels: 
Encryption:
  - Google-managed key
  - Customer-managed key

Public object url: https://storage.googleapis.com/bucket-name/object-name
Links:
- https://cloud.google.com/storage/docs/access-control/making-data-public


A resolver: 
- privacidad a nivel de objetos o bucket?

# GCS via gsutil
Es el comando utilizado para interactuar con GCS para:
- Crear buckets
- Etiquetarlos
- Subir y bajar ficheros
- ...

```bash
gsutil ls
gsutil ls gs:/bucketname
gsutil --help
gsutil mb -l <location> bucket-name
```

Links:
- https://github.com/ACloudGuru/gcp-cloud-engineer/blob/master/storage-labs/gsutil-lab-commands.txt
- https://cloud.google.com/storage/docs/locations

# GCE

Links:
- https://cloud.google.com/iam/docs/understanding-service-accounts
- https://cloud.google.com/service-usage/docs/enabled-service
- https://github.com/ACloudGuru/gcp-cloud-engineer/blob/master/compute-labs/first-vm.txt


# Roundown on gcloud
Linea de comando para interactuar con GCP
Otras lineas de comando son gsutil(GCS) y bq(GCBigquery)
In general: more powerful than console but less powerful than REST API
Alpha y Beta versions avialbel via "gcloud alpha" and "gcloud beta"

## Syntax
```
gcloud <global flags> <service/product> <group/area> <command> <flags> <parameters>

# Examples
gcloud --project myprojectid compute instances list
gcloud --project=myprojectid compute instances list
gcloud compute instances create myvm
gsutil ls
```

## Global flags
-- help
-h
--project <projectid>
--account
--filter (or GREP)
--format (JSON, YAML, CSV, etc)
--quiet

## Config properties
- Values entered once and used by any command that needs them
- Can be overridden on a specific command with corresponding flag
- ussed very often for account, project, region, and zone
  - Set "core/account" or "account" to replace "--account"
  - Set "core/project" or "project" to replace "--project"
  - Set "compute/region" to replace "--region"
  - Set "compute/zone" to replace "--zone"
- Set with _gcloud config set <property> <value>_
- Check with _gcloud config set value <property>_
- Clear with _gcloud config unset <property>_

## Configurations
- Can maintain groups of settings and switch between them
- Most useful when using multiple projects
- Iteractive workflow to set common properties in a config with _gcloud init_
- List all properties in a configruation with _gcloud config list_
- List all configurations with _gcloud config configurations list_
  - IS_ACTIVE column shows which one is currently being used
  - Other columns list account, project, region, zone, and the name of the config
- Make new config _gcloud config configurations create ITS-NAME_
- Start ussing config when _gcloud config configurations activate ITS-NAME_
  - Or use for justo one command with _--configuration=ITS-NAME_

Links:
- https://cloud.google.com/sdk/docs/configurations
- https://cloud.google.com/sdk/docs/properties
- https://cloud.google.com/sdk/gcloud/reference/
- https://cloud.google.com/sdk/gcloud/


# GCE in and out
```
# Check the elected project
gcloud config list

# Show any .ssh folder
pwd
ls
ls -a .ssh

# Get our bearings in Cloud Shell
whoami
hostname
curl api.ipify.org

# Check that we have nothing running
gcloud compute instances list

# Don't create a default VM
# Cancel: gcloud compute instances create myhappyvm

# Look at how to set the machine type
gcloud compute instances create myhappyvm -h
gcloud compute instances create myhappyvm --help
gcloud compute machine-types list

# See how to filter
gcloud topic filters

# Show some free-tier-eligible options
gcloud compute machine-types list --filter="NAME:f1-micro"
gcloud compute machine-types list --filter="NAME:f1-micro AND ZONE~us-west"

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

# Get our bearings -- Skip?
whoami
hostname
curl api.ipify.org

# Get back to Cloud Shell
exit
curl api.ipify.org

# Look at the Cloud Shell .ssh files
cd .ssh
ls
cat google_compute_engine.pub
head -n 10 google_compute_engine

# Log back onto the VM
gcloud compute ssh myhappyvm

# See that our key is authorized
cd .ssh
ls
cat authorized_keys
cd ..

# Check out the metadata
curl metadata.google.internal/computeMetadata/v1/
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/project/
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/project/project-id
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/project/attributes/
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/project/attributes/ssh-keys

# Look at some instance metadata
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/instance/
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/instance/name
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/
curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/email

# See what gcloud knows
gcloud config list

# Look at our buckets
gsutil ls
gsutil ls gs://storage-lab-cli/

# Attempt to delete the VM from within the VM
gcloud compute instances delete myhappyvm

# Exit back to Cloud Shell and actually delete the VM
exit
gcloud compute instances delete myhappyvm
```

Links:
- https://cloud.google.com/sdk/gcloud/reference/topic/filters
- https://cloud.google.com/compute/docs/storing-retrieving-metadata


10. Scaling
Se manejan mediante Instance groups, hay dos tipos:

- manejados: permiten en base a una serie de reglas escalar o no el ńumero de instancias
- no manejados: no permiten escalar

Links:
- https://cloud.google.com/compute/docs/instance-templates
- https://cloud.google.com/compute/docs/instance-groups


11.  Security
# What is "proper" data flow? CIA
- You cannot view data you shouldn't - Confidentiality
- You cannot change data you shouldn't - Integrity
- You can access data you should - Availability

# How do we control data flow? AAA
- Authentication - Who are you?
- Authorization - What are you allowed to do?
- Accounting - What did you do?

- Reesilency - Keep it running

# Key security mindset (Principles)
- Least privilege
- Defense in depth
- Fail securely
- ...

# Key Security Products/features - AuthN
- Identity
  - Humans in G suite, Cloud identity
  - Applications & services are Service Accounts
- Identity hierarchy
  - Google Groups
- Can use Google Cloud Directory Sync (GCDS) to pull from LDAP (no push)

# Key Security Products/features - AuthZ
- Identity hiearchy (Google Groups)
- Resource hierarchy (Organization, Folders, Projects)
- Identity and Access Managemente (IAM)
  - Permissions
  - Roles
  - Binding
- GCS ACLs
- Billing management
- Audit/Activity Logs (provided by Stackdrive)
- Billing export
  - To BigQuery
  - To file (in GCS bucket)
    - Can be JSON or CSV
- GSC object Lifecycle Management

Links:
- https://raw.githubusercontent.com/OWASP/Top10/master/2017/OWASP%20Top%2010-2017%20(en).pdf
- https://wiki.owasp.org/index.php/Security_by_Design_Principles
- https://www.google.com/search?q=public+bucket+breach
- https://en.wikipedia.org/wiki/Information_security


# IAM Breakdown
## Resource Hierarchy
- Resource
  - Something you create in GCP
- Project
  - Container for a set of related resources
- Folder
  - Contains any number of Projects and Subfolders
- Organization
  - Tied to G Suite or Cloud Identity domain

Links:
- https://cloud.google.com/iam/docs/overview
- https://cloud.google.com/iam/docs/resource-hierarchy-access-control


## Permissions
- A permission allows you to perform a certain action
- Each one follows the form _Service.Resource.Verb_
- Usually correspond to REST API methods
- Examples:
  - _pubsub.subscriptions.consume_
  - _pubsub.topics.publish_


## Roles
- A role is a collection of permissions to use or manage GCP resources
- Primitive roles - Project-level and often too broad
  - Viewer is read-only
  - Editor can view and chagne things
  - Owner can also control access & Billing
- Predefined roles - Give granular access to specific GCP resources
  - eg: _roles/bigquery. dataEditor, roles/pubsub.subscriber_
  - Read through the list of roles for each product!. Think about why each exists.
- Custom role - Project or Org-level collection you define of granular permissions

Links:
- https://cloud.google.com/iam/docs/understanding-roles#predefined_roles
- https://cloud.google.com/iam/docs/understanding-custom-roles
- https://cloud.google.com/iam/docs/understanding-roles
- https://cloud.google.com/iam/docs/overview


## Members
- A member is some Google- known identity
- Each member is identified by a unique email address
- Can be:
  - user: Specific Google account
    - G Suite, Cloud Identity, Gmail, or validated email
  - serviceAccount: Service account for apps/service
  - group: Google grpou of users and service accounts
  - domain: Whole domain managed by G soute or Cloud identity
  - allAuthenticatedUsers: Any Google account or service account
  - allUsers: anyone on the internet (public)


## Groups
- A google Group is a named collection of Google accounts and service accounts.
- Every group has a unique email addresss that is associated with the group
- You never act as the group
  - But membership in a grou pcan grant capabilities to individuals
- Use them for everything
- Can be used for owner when withing an organization
- Can nest groups in an organization
  - Example: one group for each departament, all those in group for all staff

Links:
- https://cloud.google.com/iam/docs/overview


## Policies
- A policy binds members to roles for some scope of resources
- Answers: Who can do what to which things?
- Attached to some level in the resource Hierarchy
  - Organization, folder, project, resource
- Roles and Members listed in policy, but resoruces indetified by attachment
- Always additive (allow) iand ndever substractive (no Deny)
  - Child policies cannot restrict access granted at a higher level

### Policies (cont.)
- One policy per resource
- Max 1500 member bindings per policy
  - Ridiculously high max
  - Anywhere close and "you are doing it wrong"
  - User groups, instead
    - not kidding
    - dont forget this
- you should use groups
- Usually takes less than 60s to apply changes (both granting and revoking)
- may take up to 7 minutes for ... changes to fully propagate across the system

Links:
- https://www.google.com/search?q=gcloud+add-iam-policy-binding+site%3Acloud.google.com
- https://cloud.google.com/iam/docs/granting-changing-revoking-access
- https://cloud.google.com/iam/docs/overview
- https://cloud.google.com/iam/docs/using-iam-securely
- https://cloud.google.com/iam/docs/faq
- https://cloud.google.com/iam/docs/overview



## Billing IAM Roles
| Role  | Purpose  | Scope  |
|---|---|---|
| Billing Account Creator  | Create new self-service billing accounts   | org  |
| Billing Account Administrator  | Manage billing accounts (but not create them)   | billing account   |
| Billing Account User  | Link projects to billing account  | Billing Account  |
| Billing Account Viewer  | View billing account cost information and transaction   | Billing Account  |
| Project Billing Manager  | Link/Unlink the project to/from a billing accoun  | Project  |


## Monthly invoice Billing
- Get billed monthly and pay by invoice due date
- can pay via check or wire transfer
- can increase project and quota limits
- Billing administrator of orgs current billing account contacts Cloud Billing Suports
  - To determine eligibility
  - to apply to switch to monthly invoicing
- Eligibility depends on
  - account age
  - typical montyly spend
  - country

Links:
- https://cloud.google.com/billing/docs/how-to/invoiced-billing
- https://cloud.google.com/billing/docs/how-to/billing-access



12. Networking

Links: 
- https://en.wikipedia.org/wiki/Routing
- https://www.webopedia.com/quick_ref/OSI_Layers.asp

# Load Balancing

Links:
- https://cloud.google.com/load-balancing/docs/load-balancing-overview