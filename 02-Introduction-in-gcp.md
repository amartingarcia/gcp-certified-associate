# Introduction in GCP
## GCP Context
### History of GCP
- Grew some services internally
  - Built by Googlers for Google
  - Not originally for Enterprise
- Purchased some services
  - Leaks in abstractions more evident
- Catch-up to AWS
  - Some functionality missing
  - Avoided some mistake
  - More willing to be "a cloud" that you use, not just "the cloud" that you use

### Links Section
- [SRE Books](https://landing.google.com/sre/books/)
- [Interview with Lynn Langit](https://read.acloud.guru/serverless-superheroes-lynn-langit-on-big-data-nosql-and-google-versus-aws-f4427dc8679c)
- [Google Tools](https://en.wikipedia.org/wiki/Google_data_centers#Software)

## GCP Desing and Structure
### Desing Principles:
* Global
* Secure
* Huge scale
* For developers

### Global System:
* GCP is intrinsically global
* AWS is intrinsically region-scoped
* Regional model
  * Simplifies data sovereignty
* Global model
  * Easier to hanlde latency and failures in a global way
  * Could be more sensitive to multi-region/global failure modes
    * (Due to service failures, not underlying hardware issues)

### Physical Infrastructure:
* vCPU
* Physical server
* Rack
* Data center (building)
* Zone
* Region
* Multi-region
* Private global network
* Points of Presence (POPs) - Network edges and CDN locations

### Global Regions
![Global regions](img/global_regions.png)

### Network Ingress & Egress
* Normal newtork: Routes via Internet to edge location closest to __destination__
* Google: Routes so traffic enters form Internet at edge closest to __sources__
  * Enables very interesting scenarios
  * Since global IP address con load balance worlwide
  * Sidesteps many DNS issues
* Can now opt for "normal" network routing to reduce price (and functionality)

### Princing
* Provisioned - "Make sure you are ready to handle X"
* Usage - "Handle whatever I use, and charge me for that"
* Network traffic
  * Free on the way in (ingress)
  * Charged on the way out (egress), by BGs used
  * Egress to GCP services sometimes free
    * Depends on the destination service
    * Depends on the location of that service

### Security
* Separation of duties and physical security
* Absolutely everyting always encrypted at rest
* Strong key and identity management
* Network encryption
  * All control info encrypted
  * All WAN traffic to be encrypted automatically
  * Moving towards encrypting all local traffic within data centers
* Distrust the network, anyway
  * BeyondCorp

### Scale and Automation
* Scalability must be unbounded
* Devs dont want to answer pages

### Resource Quotas (Soft Limits)
* Scope
  * Regional
  * Global
* Changes
  * Automatic
  * By request
    * Response in 24-48h
    * May be refused
* Queryable
  * `gcloud compute project-info describe --project myprojectid`

### Organization
* Projects are similar to AWS accounts
* Projects own resources
* Resources can be shared with other projects
* Projects can be grouped and controlled in a hierarchy

### Links Section
- [Data Center Tour #1](https://www.youtube.com/watch?v=XZmGGAbHqa0)
- [Data Center Tour #2](https://www.youtube.com/watch?v=zDAYZU4A3w0)
- [Region Maps](https://cloud.google.com/about/locations/#regions-tab)
- [Region and Zones Docs](https://cloud.google.com/compute/docs/regions-zones/)
- [Network Maps](https://cloud.google.com/about/locations/#network-tab)
- [Global Load Balancing](https://cloud.google.com/load-balancing/docs/https/)
- [Network Pricing](https://cloud.google.com/compute/all-pricing#network)
- [Pricing Calculator](https://cloud.google.com/products/calculator/)
- [BeyondCorp](https://cloud.google.com/beyondcorp/)
- [GCP Security Desing](https://cloud.google.com/security/infrastructure/design/)
- [Summary article on SRE Principles](https://medium.com/@jdavidmitchell/principles-of-site-reliability-engineering-at-google-8382b054e498)
- [Resources Quotas (Soft Limits)](https://cloud.google.com/compute/quotas)

