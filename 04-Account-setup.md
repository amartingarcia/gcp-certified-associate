# Account Setup
## Free-tier GCP Accounts
* Billing Account that does not get charged
  * Must be manually upgrade to a paying account
  * Still requires a credit card, for verification
* $300 USD credit that cn last 12 months
  * "When your trial ends, your account wil be paused and you will have the option to upgrade to a paid account"
* Excellent for learning
* "Bussines accounts are not elegible for the free trial"
* Has some restrictions

### Free Trial Restrictions
* No more than 8 vCPUs (total simultaneous)
* No GPUs (video card chips)
* No TPUs (custom chips for TensorFlow)
* No Quota increase
* No cryptomining allowed
* No SLAs
* No premium OS licenses (eg Windows)
* No Cloud Launcher products with extra usage free

### "Always Free"
* "Always Free usage does not count against your free trial credits"
* Last beyond end of free trial

### "Always Free" Compute Highlights
* 24h/day of f1-micro runtime, _in most US regions, only_
* 28h/day of App Engine runtime, _in North America_
* 2M/month of Cloud Functions invocations (with rutntime/size limits)

### "Always Free" Compute Highlights
* Storage averaged over the month
* 5 GB of Regional Cloud Storage, including some operations
* 1 GB of Cloud Datastore, including some operations
* 10 GB of BigQuery storage, with 1TB/month of query processing
* 30 GB HDD storage on GCE (Google Compute Engine) and AE (App Engine)
* 5 GB snapshot storage on GCE (Google Compute Engine) and AE (App Engine)
* 5 GB of StackDriver logs with 7 day retention

### "Always Free" Networking Highlights
* _Egress to China and Australia not free!_
* 1 GB/month of App Engine data egress
* 1 GB/month of Compute Engine data egress
* 5 GB/month of egress by Cloud Function invocations
* 5 GB/month of egress from Cloud Storage based in North Amercia
* 10GB/month of Cloudf PubSub messages

### "Always Free" Other Highlights
* 120 build-minutes/day of Google Cloud Container Builder
* 60 minutes/month of Google Cloud Speech API recognition form audio/video
* 1000 units/month of Clouf Vision API Calls
* 5000 units/month of Google Cloud Natural Lenguage API
* Google Cloud shell with 5 GB of persistent disk storage quota
* 1 GB of Google Cloud Source Repositories private hosting

### Links Section
- [GCP Free Trial](https://cloud.google.com/free/)
- [Free Trial Restriction](https://cloud.google.com/free/docs/gcp-free-tier#limitations)
- ["Always Free"](https://cloud.google.com/free/docs/gcp-free-tier)

## Explore GCP Console
### Links Section
- [Google Cloud Status](https://status.cloud.google.com/)

## Set Up Billing Export
Tools for monitoring, analyzing and optimizing cost have become an important part of managing development. Billing export to Big query enables you to export your daily usage and cost estimates automatically throughout the day to a BigQuery dataset you specify. You can then access your billing data from BigQuery.

* Export must be set up per billing account
* Resoureces should be placed into appropiate projects
* Resources should be ttagged with labels
* Billing export is not real-time
  * Delay is hours

### Links Section
- [Billing Export](https://cloud.google.com/billing/docs/how-to/export-data-bigquery)

## Set Up Billing Alert
To help you with project planning and controlling costs, you can set a budget. Setting a budget lets you track how your spend is growing toward that amount.

You can apply a budget to either a billing account or a project, and you can set the budget at a specific amount or math it to the previous months spend. You can also create alerts to nofify billing administrators when spending exceeds a percentage of your budget.

### Links Section
- [Budgets](https://cloud.google.com/billing/docs/how-to/budgets)

## Set Up Non-Admin Access User
### Billing IAM
* __Role__: Billing Account User
* __Purpose__: Link projects to billing accounts
* __Level__: Organization or billing account
* __Use Case__: This role has very restricted permissions, so you can grant it broadly, typically in combination with Project Creator. These two roles allow a user to create new projects linked to the billing account on which the role is granted

### Setting UP
* Get email address of __non-admin__ Google account you control
  * Not the admin account we created when signing up for GCP
  * This wiel be our "user" account
  * Could be pre-existing Google account
  * Could make Google account for any existing email address
  * Could make new Gmail account

### Links Section
- [Billing Access](https://cloud.google.com/billing/docs/how-to/billing-access)