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

