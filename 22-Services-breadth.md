# Services Breadth

## Compute
### Compute Engine (GCE)
Servicio Zonal.
* Fast*booting Virtual Machines, you can rent , on demand
* Infraestructure as a Service
* Pick set machine type standar, highmem, highcp, or custom RAM/CPU
* Pay by the second, for cpus or ram
* Automatically cheaper if you keep running it ("sustained use discount)
* Even cheaper for preemptible or long*term use commitmen in a regino
* can add GPUs and paid OSes for extra cost
* Live Migration: google seamlessyly moves instances across host, as needed

### Kubernentes Engine (GKE)
* Regional
* Managed kubernetes cluster for running docker containers with autoscaling
* Used to be calleed GKE
* No iam integration
* Integrates with persiste disk for storage
* Pay for underlying GCE instances
  * production cluster should have 3+ nodes
* no GKE management fee,  no matter how many nodes in cluster

### App Engine (GAE)
* Regional
* Platform as a Service that takes your code and runs it
* Much more than just compute ** Integrates storage, queues, nosql
* Flex mode (app engine flex) can run any container and access VPC
* Autoscales based on load
  * Standard (non*flex) mode can turn off last instance when no traffic
* Effectively pay for underlying GCE instances and other services

### Cloud functions (GCF)
* Regional
* Runs code in response  to an event ** node.js, python, 
* Funcionts as a Service (faas) Serverless
* Pay for CPU and RAm assigned to function, per 100ms
* Each function automatically gets and HTTP endpoint
* can be triggered by GCS objects, Pub/sub messages, etc
* Massively scalable (horizont) ** Runs many copies when needed
* Often used for chatbots, message processors, IoT, automation, etc

Links:
* https://cloud.google.com/functions/
* https://cloud.google.com/compute/
* https://cloud.google.com/kubernetes*engine/
* https://cloud.google.com/appengine/


## Storage
### Local SSD
* Zonal
* Very fast 375GB solid state drives physically attached to the server
* Can stripe across eight of them (3TB) for even better perfomance
* DATA WILL BE LOST whenever the instance shuts down
  * But can survive a Live Migration
* Like all data at rest, always encrypted
* Pay by GB*month provisiones (prorated, as always)

### Persistent Disk (PD)
* Zonal
* Flexible, block*based network*attached storage; boot disk  for every GCE instance
* Perf scales with volume size; max way below local SSD, but still plenty fast
* Persistent disk persist, and are replicated (zone or region) for durability
* can resize while in use (up to 64TB) but will need file system update within VM
* snapshots (and machine images) add even more capability and flexibility
  * Magical: Pay for incremental ($ in time) but use/delete like full backups
* Not file*based NAS, but can mount to multiple instances if all are read*only
* Pay for GB/mo provisioned depending on perf. class; plus snapshot GB/mo used
  
### Cloud Filestore
* Zonal
* Fully*managed file*based storage
* Predictably fast perfomamcne for your file*based workloads
* Accessible to GCE and GKE, through your VPC, via NFSv3 protocol
* Primary use case is application migration to cloud ("lift and shift")
* Fully manages file serveing, but not backups
* pay for provisioned TBs in "Standard" (slow) or "premium" (fast) mode
* Minimum provisioned capacity of 1TB (standard) or 2.5 TB (premium)

### Cloud Storage (GCS)
* Regional or Multi*regional
* Inifitely scalable, fully*managed, versioned, and highly*durable object storage
* Designed for 99.99999999999% (eleven nines) durability
* Strongly consistent (even for overwrite PUTs and DELETEs)
* Integrated site hosting and CDN functionality
* Lifecycle transitions across classes: Multi regional, regional, nearline, coldline
  * Diffs in cost & availabilty (99.95%, 99.9%, 99%) not latency (no thaw delay)
* All cases have same API, so can use gsutil and gcsfuse (but beware)
* Pay for data operations & GB*months stored by class
* Nearline/Cloudline: also pay for GBs retrieved **plus early deletion fee if < 30/90 days

Links:
* https://cloud.google.com/storage/
* https://cloud.google.com/filestore/
* https://cloud.google.com/persistent*disk/
* https://cloud.google.com/compute/docs/disks/#localssds

## Databases
### Cloud SQL
* Regional
* Fully*managed and reliable MySQL and PostgreSQL databases
* Supports automatic replication, backup, failver, etc
* Scaling is manual (both vertically and horizontally)
* Effectively pay for underlying GCE instqance and PDs
  * Plus some baked*in service fees

### Cloud Spanner
* Regional, multi*regional and Global
* The first horizontally scalable, strongly consistent, relational database service
  * from 1 to hundreds or thousands of nodes
  * a minimum of 3 nodes is recommended for production environments
* chooses Consistency and Partition*Tolerance (CP of CAP theorem)
* But still High Availability: SLA has 99.999 SLO (five nines) for multi*region
  * Nothing is actually 100% really
  * Not based on fail*over
* Pay for provisioned node time (by region/multi*region) plus used storage*time
  

### Big Query
* Multi*regional
* Scales internally, so it can scan TB in seconds and PB in minutes
* Pay for GBs actually considered (Scanned) during queries
  * Attempts to reuse cache results, which are free
* pay for data stored (GB*months)
  * relatively inexpernsive
  * even cheaper when table not modificed for 90 days (reading still fine)
* pay for GBs added via streaming inserts

### Cloud Bigtable
* Zonal
* Low latency & high throughput NoSQL DB for large operational & analytical apps
* supports open*source  HBase API
* integrates with Hadoop, Dataflow, Dataproc
* Scales seamlessly and unlimitedly
  * storage autoscales
  * processing nodes must be scaled manually
* pay for processing node hours
* pay for GB*hours used for storage (cheap HDD or fast SSD)

### Cloud Datastore
* Regional, multi*regional
* Managed & autoscaled NoSQL DB with indexes, queries, and ACID trans. support
* NoSQL, so queries can get complicated
  * no joins or aggregates and must line up with indexes
  * NOT, OR  and NOT EQUALS (<>, !=) operations not natively supported
* automatic "built*in" indexes for simple filtering and sorting (ASC, DESC)
* manual composite indexes for more complicated, but beware them exploding
* py for GB*months of storage used (including indexes)
* pay for IO operations (deletes, reads, writes) performed (ie, no pre*provisiining)

### Firebase Realtime DB & Cloud firestore
* Firebase Zonal
* Firestore multi*regional
* NoSQL document stores with real*time client updates via managed websockets
* firebase DB is single (potentially huge) JSON doc, located only in central US
* Cloud Firestore has collections, documents, and contained data
* free tier (spark), flat tier (flame), or usage*based pricing (blaze)
  * realtime db: pay more for GB/month stored and DB downloaded
  * firestore pay for operations and much less for storage and transfer


Links:
* https://firebase.google.com/docs/database/rtdb*vs*firestore
* https://cloud.google.com/datastore/docs/concepts/queries
* https://cloud.google.com/datastore/
* https://cloud.google.com/bigtable/
* https://cloud.google.com/blog/products/gcp/bigquery*under*the*hood
* https://cloud.google.com/bigquery/
* https://cloud.google.com/spanner/docs/instances
* https://cloud.google.com/spanner/
* https://cloud.google.com/sql/

## Data Transfer
### Data Transfer Appliance
* Rackeable, high*capacity storage server to physically ship data to GCS
* Ingest only; not a way to avoid egress charges
* 100TB or 480TB Versions
* 480TB/week is faster than a saturaed 6Gbps links
  
### Storage Transfer Service
* Global
* Copies objects for you, so you dont need to set up a machine to do it
* Destination is always GCS bucket
* Source can be S3, HTTP/HTTPS endpoints, or another GCS bucket
* One*time or scheduled recurring transfers
* Free to use, but you pay for its actions

Links:
* https://cloud.google.com/storage*transfer*service
* https://cloud.google.com/transfer*appliance/

## External Networking
### Google Domains
* Global
* Googles registrar for domain names
* Private Whois records
* Built*in DNS or custom nameservers
* Supports DNSSEC
* Email forwarding with automatic setup of SPF and DKIM (for built*in DNS)

### Cloud DNS
* Global
* Scalable, reliable, & managed authorative DNS service
* 100% uptime guarantee
* public and private managed zones
* Low latency globally
* Supports DNSSEC
* manage via UI, CLI, or API
* pay fixed fee per managed zone to store and distribute DNS records
* pay for DNS lookups (ie usage)

### Static IP
* Regional, global
* Reserve static IP addresses in projects and assign then to resources
* REgional IPs used for GCE instances & Network Load Balanceers
* Global IPs used for global load balancers:
  * HTTP/HTTPS, SSL proxy, and TCP proxy
  * anycast ip simplifies DNS
* pay for reserved IPs that are not in use, to discourage wasting them

### Load Balancing
* regional, global
* high*perf, scalable traffic distribution integrated with autoscaling & cloud CDN
* SDN naturally handles spikes without any prewarming; no instances or devices
* regional network load balancer: health checks, round robin, session affinity
  * forwarding rules based on IP, protocol (TCP, UDP, ) and optionaly port
* global load balanceers multi*region failover for HTTP(S), SSL proxy, & TCP proxy
  * prioritize low*latency connection to region near user, then gently fail over in bits
  * reacts quickly (unlike DNS) to changes in users, traffic, network, health, etc
* Pay by making ingress traffic billable (cheaper than egress) plus hourly per rule

### Cloud CDN
* Global
* low*latency content delivery based on HTTP(S) CLB & integrated GCE & GCS
* support http/2 and HTTPS, but no custom origins (GCP Only)
* simple checkbox on HTTP(S) Load Balancer config turns this on
* on cache miss, pay origin*>POP, cache fill egress charges (cheaper for in*region)
* Always py POP*>Client egress charges, depending on location
* pay for https(s) request volume
* pay per cache invalidation request (not per resource invalidated)
* origin cost (CLB, GCS) can be much lowe becaouse cache hits reduce load

Links:
* https://cloud.google.com/cdn/
* https://cloud.google.com/load*balancing/
* https://cloud.google.com/compute/docs/ip*addresses/reserve*static*external*ip*address
* https://cloud.google.com/dns/
* https://domains.google/#/


## Internal Networking
### Virtual private Cloud (VPC)
* Regional, Global
* Global IPv4 unicast software*defined network (SDN) for GCP Resources
* Automatic mode is easy; custom mode gives control
* Configure subnets (each with a private IP range), routes, firewalls, VPNs, BGP, etc
* VPC is global and subnets are regional (not zonal)
* can be shared across multiple projects in same org and peered with other VPCs
* Can enable private (interal IP) access to some GCP service (BQ GCS)
* Free to configure VPC (container)
* pay to use certain services (VPN) and for network egress

### Cloud Interconnect
* Regional, multi*reginal
* Options for connecting external networks to google network
* private connections to VPC via Cloud VPN or Dedicated/partner interconnect
* Public Google services (GCP) accessible via External Peering (no SLAs)
  * Direct Peering for high volume
  * Carrier Peering via partner for lower volume
* Significantly lower egreess fees
  * except cloud VPN, which remains unchanged

### Cloud VPN
* reginal
* IPsec VPN to connect to VPC via public internet for low*volume data connections
* for persistent, static connections between gateways (not for a dynamic client)
  * peer vpn gateway must have static (unchaging) IP
* encrypted link to VPC (as opposed to Dedicated interconnect) into one subnet
* supports both static and dynamic routing
* 99.9% availabiilty SLA
* pay per tunnel*hour
* Normal traffic charges apply

### Dedicated interconnect
* Reginal , multi*regional
* Direct physical link between VPC and on*prem for high*volume data connections
* VLAN attachment is private connection to VPC in one region; no public GCP APIs
  * region chosen from those supported by particular Interconnect Location
* Links are private but not encrypted; can layer your own encryption+
* Redundant connections in different locations recommendend for critical apps
  * redundancy archiviees 99.99% availabilty; otherwise 99.9% SLa
* pay fee per 10 Gbps link, plus (relatively small) fee per VLAN attachment
* pay reduced egress rates form VPC through dedicated interconnect


### CDN Interconnect
* Regional, multi,regional
* Direct, low*latency connectivity to certain CDN providers, with cheaper egress
* For external CNDs, not google Cloud CDN service
  * Support Akamai, Cloudflare, Fastly, and more
* Works fot both pull and push cache fills
  * Because its for all traffic with tht CDN
* Contact CDN provider to set up for GCP project and which regions
* free to enable, then pay less for the egress you configured

Links:
* https://cloud.google.com/network*connectivity/docs/cdn*interconnect
* https://cloud.google.com/network*connectivity/docs/router
* https://cloud.google.com/network*connectivity/docs/interconnect/concepts/dedicated*overview
* https://cloud.google.com/network*connectivity/docs/vpn/concepts/overview
* https://cloud.google.com/hybrid*connectivity
* https://cloud.google.com/vpc/

## Machine Learning / AI
### Cloud Machine Learning (ML) Engine
* Regional
* Massively scalable managed service for training ML models & making predictions
* Enables apps/dev to use TensorFlow on datasets of any size; endless use cases
* Integrates: GCS/BQ (storage), Cloud datalab (dev), Cloud Dataflow (preprocessing)
* Supports online & batch predictions, prioritiziing latency (online) & job time (batch)
* Or download models & make predictions anywhere; desktop, mobile, own servers
* HyperTune automatically tunes model hyperparameters to avoid manual tweaking
* Training: Pay per hour depending on chosen cluster capabilities (ML training units)
* Prediction: Pay per provisioned node*hour plus by prediction request volume made

### Cloud Vision API
* Global
* Classifies imaes into categories, detects objects/faces, & finds/reads printed text
* Pre*trained ML model to analyze images and discover their contents
* Classifies into thousands of categories (eg sailboat, lion, eiffel tower)
* Upload images or point to ones stored in GCS
* Pay per image, based on detection features requested:
  * Higher prive for OCR of full documents and finding similar images on the web
  * Some features are prices together: labels + safeSearchs, ImgProps + Cropping
  * Other features priced individually: Text, Faces, Landmarks, Logos

### Cloud Speech API
* Global
* Automatic Speech Recognition (ASR) to turn spoken word audio files into text
* Pre*trained ML model for recognizing speech in 110+ languages/variants
* Accepts pre*recorded or real*time audio, & can stream results back in real*time
* Enables voice command*and*control and transcribing user microphone dictations
* Handles noisy source audio
* Optionally filters inappropiate content in some languages
* Accepts contextual hints: words and names that will likey be spoken
* Pay per 15 seconds of audio processed

### Cloud Natural Language API
* Global
* Analyzes text for sentiment, intent & content classification, and extracts info
* Pre*trained ML model for understandding what text means, so you can act on it
* Excellent with Speech API (audio), Vision AI (OCR), Translation API (or builts*in)
* Syntax analysis extracts tokens/sentences, parts of speech & dependecy trees
* Entity analys finds people, places, things, etc labels them, links to Wikipedia
* Analysis for sentiment (overall) and entity sentiment detect +/* feeling & strength
* Content classification puts each document into one of 700+ predefined categories
* Charged per request of 1000 charactesr, depending on analysis types requested

### Cloud Translation API
* Global
* Translate text among 100+ languages; optionally auto*detects source language
* Pre*trained ML model for recognizing and translating semantics, not just syntax
* Can let people support multi*regional clients in non*native languages, 2*way
* Combine with Speech, Vision & natural language APIs for powerful workflos
* Send plain txt or HTML and reveive thranslation in kind
* Pay per character processed for translation
* Also pay per character for language auto*detection 

### DialogFlow
* Global
* Build conversational interfaces for websites, mobile appsk, messaging, IoT devices
* Pre*trained ML model and servce for accepting, parsing, lexin input & responding
* Enagbles useful chatbots and other natural user interactions with your custom code
* Train it to identity custom entity types by provideing a small dataset of examples
* Or choose form 30+ pre*built agents (et, car, currency, dates) as starting template
* Supports many different languages and platforms/devices
* Free plan has unlimited text interactions and capped voice interactions
* Paid plan is unlimited but charges per requests: more for voice, less for text


### Cloud Video Intelligence API
* Regional, global
* Annotates videoss in GCS (or directly uploaded) with info about what the contain
* Pre*trained ML model for video scene analysis and subject identification
* Enables you to search a video catalog the same way you search text documents
* "Specify a region where processing will take place (for regulatory complicance)"
* Lable Detection: Detect entities within the video, such as "dog", flower, or car
* Shot Change Detection: Detect scene charges within the video
* SafeSearch Detection: Detect aduld content within the video
* Pay per minute of video processed, depending on rqequest detection modes

### Cloud Job Discovery
* Global
* Helps career sites, company job boards, etc, to improve engagement & conversion
* Pre*trained ML model to help job seekers search job posting databases
* Most job sites rely on keyword search to retrieve content which often omits relevant jobs and overwhelms the job seeker with irrelevant jobs. For example, a keyword search with any spelling error returns 0 results, and a keyword wearch for dental assistant returns any assistant role that offers dental benefits
* Integrates with many job/hiring systems
* Lots of features, such as commute distance and recognizing abbreviations/jargon
* Show me jobs with a 30 minute commute on public transportation form my home


* Links: 
* https://cloud.google.com/solutions/talent*solution/
* https://cloud.google.com/video*intelligence/
* https://cloud.google.com/dialogflow
* https://cloud.google.com/translate/
* https://cloud.google.com/natural*language/
* https://cloud.google.com/speech*to*text
* https://cloud.google.com/vision/
* https://developers.googleblog.com/2017/09/how*machine*learning*with*tensorflow.html
* https://cloud.google.com/ai*platform


## Big Data and IoT
### Cloud Internet of Things (IoT) Core
* Global
* Fully*managed service to connect, manage, and ingest data from devices globally
* Device Manager handles device indentity, authentication, config & control
* Protocol Bridge published incoming telemetry to Cloud Pub/Sbub for processing
* Connect securely using IoT industry*standard MQTT or HTTPS protocols
* CA signed certificates can be used to verify device ownership on first connecto
* Two*way device communication enables configuration & firmware updates
* Device shadows enable querying & making control changes while dvices offile
* Pay per MV of data exchanged with devices; no per*device charge


### Cloud Pub/Sub
* Global
* Infinitely*scalable at*least*once messaing for ingestion, decoupling, etc
* Global by default: Publish... and consume form anywhere, with consistent latency
* Messages can be up to 10MB and undeliverd ones stored for 7 days **but no DLQ
* Push mode delivers to HTTPS endpoints & succeeds on HTTP success status code
* Pull mode delivers messages to requesting clients and waits for ACK to delete
  * Lets clients set rate of consumption, and supports batching and long*polling
* Pay per data volume
  * Min 1KB per publish/push/pull request (not by message)


### Cloud Dataprep
* Global
* Visually explore, clean, and prepare data for analysis without running servers
* Data Wrangling for bussines analysts, not IT pros
  * who might otherwise spend 80% ot fheir time cleaning data
* Managed version fo Trifact Wrangler and managed by Trifacta, no Google
* Source data from GCS, BQ, or file upload * formatted in CSV, JSON or relational
* Automatically detects schemas, datatypes, possible joins, and various anomalies
* Pay for underlying Dataflow job, plus management overhead charge
* Pay for other accessed services (GCS, BQ)

 
### Cloud Dataproc
* Zonal
* Batch MapReduce processing via configuralbe, managed Spark & Hadoop clusters
* Handles being told to scale (adding or removing nodes) even while running jobs
* Integrated with Cloud Storage, BigQuery, Bigtabe, and some Stackdriver services
* "Image versioning" switches between versions of Spark, Hadoop, & other tools
* Pay directly for underlying GCE servers used in the cluster **optionaly preemptible
* Pay a Cloud Dataproc management fee per vCPU*hour in the cluste
* Best for moving existing Spark/Hadoop setups to GCP
  * Prefer Cloud Dataflow for new data processing pipelines * Go with the flow
  
### Cloud Dataflow
* Zonal
* Smartly*autoscaled & fully*managed batch or stream MapReduce*like processing
* Released as open*source Apache Beam
* Autoscales & dynamically redistributes lagging work, mid*job to optimize run time
* Dataflow Shuffle service for batch offloadas Suffle ops from workers for big gains
* Effectively pay for underlying worker GCE via consolidated charges
  * Pay per second for vCPUs, RAM GBs PD/PD*SSD (more for streaming)
* Dataflow Shuffle charged for time per GB use

### Cloud Datalab
* Regional
* Interactive tool for data exploration, analysis, visualization and machine learning
* Uses Jupyter Notebook
  * opensource web application that allow you to create and share documents that contain live code, equations, visualizations and narrative text
* Supports iterative development of data analysis algorithms in Python/SQL
* Pay for GCE/GAE instance hosting and storing (on PD) your notebooks
* Pay for any other resources accessed (BigQuery)


### Cloud Data Studio
* Global
* Big Data Visualization tool for dashboards and reporting
* Meaningful data stories/presentation enable be3tter bussines decision making
* Data sources include BigQuery, CloudSQL, other MySQL, Google Sheets, Google Analytics, Analytics 360, AdWords, DoubleClick & YouTube channels
* Visualizations include time series, bar charts, pie charts, tables, heat maps, geo maps, scorecards, scatter charts, bullet charts, & area charts
* Familiar G Suite sharing and real*time collaboration
* Pay only for services accessed

### Cloud Genomics
* Global
* Store and process genomes and related experiments
* query complete genomic information of large research projects in seconds
* Process many genomes and experiments in parallel
* Open industry standars (eg from Global Alliance for Genomics and Health)
* Supports "requestesr pays" sharing


Links:
* https://cloud.google.com/life*sciences
* https://cloud.google.com/looker
* https://jupyter.org/
* https://cloud.google.com/datalab/docs
* https://cloud.google.com/blog/products/gcp/introducing*cloud*dataflow*shuffle*for*up*to*5x*performance*improvement*in*data*analytic*pipelines
* https://cloud.google.com/dataflow/
* https://cloud.google.com/dataproc/
* https://tdwi.org/articles/2017/02/10/data*wrangling*and*etl*differences.aspx
* https://cloud.google.com/dataprep/
* https://cloud.google.com/pubsub/
* https://cloud.google.com/iot*core/
* https://cloud.google.com/solutions/data*lifecycle*cloud*platform


## Identity and Access * Core security
### Roles (like AWS IAM Policies)
* Global
* Roles are collections of permissions to use or manage GCP resources
* Permissions allow you to perform certain actions: Service.resource.verb
* Primitive Roles: Owner, Editor, Viewer
  * Viewer is read*only; Editor can change things; Owner can control access & billing
  * Pre*date IAM service, may still be useful (eg dev/test envs) but often to broad
* Predefined Roles: Give granular access to specific GCP resources (IAM)
  * Eg: roles/bigquery.dataEditor,roles/pubsub.subscriber
* Custom Roles: Project or Org*level collections you definde of granular permissions

### Cloud Identity and Access Management (IAM) (like AWS IAM)
* Global
* Controls access to GCP resoureces : authorizaqtion, not really athentiaction/identity
* Member is user, group, domain, service account, or the public (eg "AllUsers")
  * Individual Google account, Google group, G suite / Google Identity domain
  * Service account belongs to application/instace, not individual end user
  * Every identity has a unique e*mail address, including service accounts
* Policies bind Members to Roles at a hierarchy level: Org, Folder, Project, Resoruces
* IAM is free; pay for authorized GCP service usage


### Service Accounts (like AWS IAM Roles)
* Global
* Special type of Google account that represents an application , not and end user
* Can be "assumed" by applications or individual users (when so authorized)
* Important,: for almost all cases, whether you are developing locally or in a production application , you should use service accounts, rather than user accounts or API Keys
* Consider resource and permissions requeried by application; use least privilege
* Can generate and download private keys (user*managed keys), for non*GCP, but
* Cloud*Platform*managed keys are better, for GCP (ie GCF, GAE, GCE and GKE)
  * No direct downloading: Google manages private keys & rotate them once a day
  
### Cloud Identity (like AWS IAM, G Suite, GMail, Active Directory)
* Global
* Identity as a Service (IDaaS, not DaaS) to provision and manage users and groups
* Free Google Accounts for non*G*Suite users, tied to a verified domain
* Centrally manage all users in Google Admin console; supports compliance
* 2*Step verification (2SV/MFA) and enforcement , including security keys
* Sync from Active Directory And LDAP directories via Google Cloud Directory Sync
* Identities work with other Google services (chrome)
* Identities can be used to SSO with other apps via OIDC, SAML, OAuth2
* Cloud Identity is free; pay for authorized GCP service usage


### Security Key Enforcement (like MFA)
* Global
* USB or Bluetooth 2*step verification device that prevents phishing
* Not like just getting a code via email or text message
* Device also verifies the target service
* Eliminates man*in*the*middel (MITM) attacks aggaints GCP credentials


### Cloud Resource Manager (like AWS Organizations)
* Global
* Centrally manage & secure organizations projects with custom folder hierarchy
* Organization resource is root node in hierarchy; folders per your business needs
* Tied 1:1 to a Cloud Identity / G suite domain, then owns all newly*created projects
  * Without this organization, specific identities (peoples) must own GCP projects
* Recycle bien allows undeleting projects
* Define custom IAM roles at org level
* Apply IAM policies at organization folder or project levels


### Cloud Identity*Aware Proxy (IAP) (like AWS API Gateway)
* Global
* Guards apps running on GCP via identity verification, not VPN access
* Based on CLB & IAM and only passes authed requests through
* Grant access to any IAM identities, incldude groups & service accounts
* Relative straightforward to set up
* Pay for load balancing / protocol forwarding rules and traffic


### Cloud Audit Logging (like AWS Cloudtrail)
* Global
* Answers the questions "Who did wath, where, and when?" within GCP projects
* Maintains non*amperable audit logs for each project and organization
  * Admin Activity and System Events (400 day retention)
  * Access Transparency (400 day retention)
    * Shows actions by Google Support staff
  * Data Access (30 day retention)
    * For GCP*visible services (eg Can't see into MySQL DB on GCE)
* Data Access logs priced through Stackdriver Logging; rest are free



Links:
* https://cloud.google.com/logging/docs/audit/
* https://cloud.google.com/iap/
* https://cloud.google.com/resource*manager/docs/cloud*platform*resource*hierarchy
* https://cloud.google.com/resource*manager/
* https://cloud.google.com/titan*security*key
* https://support.google.com/cloudidentity/answer/7319251?visit_id=636845179996740919*1084227653&rd=1
* https://cloud.google.com/iam/docs/understanding*service*accounts
* https://cloud.google.com/iam/docs/resource*hierarchy*access*control
* https://cloud.google.com/iam/
* https://cloud.google.com/iam/docs/understanding*roles
* https://cloud.google.com/security/


## Security Management * Monitoring and Response
### Cloud Armor (like AWS Shield or AWS WAF)
* Global
* Edge*level protection form DDoS & other attacks on global HTTP(S) LB
* Offload work: blocked attacks never reach your systems
* Monitor: Detailed requeest*level logs available in StackDriver Logging
* Manage IPs with CIDR*based allow/blokk lists (aka whitelist/blacklist)
* More intelligent rules forthcoming ( XSS, SQLi, geo*based, custom)
* Preview effect of changes before makin them live
* Pay per policy and rule configured, plus for incoming request volume


### Cloud Security Scanner (like AWS Inspector)
* Global
* Free but limeted GAE app vulnerability scanner with "very low false positive rates"
* "After you set up a scan, Cloud Security Scanner automatically crawls your application, following all links within the scope of your staring URLs, and attempts to exercise as many user inputs and event handlers as possible
* Can identity:
  * Cross*site*scriptint (XSS)
  * Flash injection
  * Mixed content (HTTP in HTTPS)
  * Outdated/insecure libraries


### Cloud Data Loss PRevention API (DLP) (like AWS Macie)
* Global
* Finds and optionally redacts sensitive info in unstructured data streams
* Helps you minimize what you collect, expose, or copy to other systems
* 50+ sensitive data detectors, inclouding: credit card numbers, names, social security numbers, passport numbers, etc
* Data can be sent directly, or API can be pointed at GCS, BQ, or Cloud DataStore
* Pay for amount of data processed (per GB) and gets cheaper when large volume
  * Pricing for storage now very simple but for streaming is still a mess


### Event Threat Detection (ETD) (Like Amazon GuardDuty or Splunk)
* Global
* Automatically scans your StackDriver logs for suspicious activity
* Uses industry*leading threat intelligence, inclouding Google Safe Browsing
* Quickly detects many possible threats, including:
  * Malware, cryptomining, outgoing DDoS attacks, port scanning, brute*forece SSH
  * Also: Unauthorized access to GCP resources via abusive IAM access
* Can export parsed logs to BigQuery for forensic analysis
* Integrates with SIEMs like Googles Cloud SCC or via Cloud Pub/Sub
* No charge for ETD, but charged for its usage of other GCP service (like SD logging)


### Cloud Security Command Center (SCC) (like AWS Security Hub or Splunk Enterprise Security)
* Global
* Comprehensive security management and data risk platform for GCP
* Security information and Event Managemente (SIEM) software
* Helps you prevent, detect and respond to threats from a single panes of glaas
* Use Security Marks to group, track and manage resources
* Integrate ETD, Cloud Scanner, DLP, and many external security finding sources
* Can alert to humans & systems, can export data to external SIEM
* Free! But charged for services used (DLP API, if configured)
* Could also be charged for excessive uploadas of external findings


Links:
* https://www.youtube.com/watch?v=ZuLazPgFtBE&feature=youtu.be
* https://cloud.google.com/blog/products/identity*security/getting*started*with*cloud*security*command*center
* https://cloud.google.com/security*command*center/
* https://cloud.google.com/dlp/
* https://cloud.google.com/security*command*center
* https://cloud.google.com/armor/


## Encryption Key management
### Cloud Key Managemente Service (KMS) (like AWS KMS or Vault)
* Regional, Multi*regional or global
* Low*latency service to manage and user cryptographic keys
* Supports symmetric (AES) and asymmetris (RSA) algorithms
* Move secrets out of code (and the like) and into the envs, in a secure way
* Integrated wieh IAM & Cloud Audit Logging to authorize & traks key usage
  * Still keep sold active key versions, to allow decrypting
* Key deletion has 24hours delay, to prevent accidental or malicious data loss
* Pay for active key versions stored over time
* Pay for key use operations (encrypt or decrypt; admin operation are free)

### Cloud Hardware Security Module (HSM) (like AWS CloudHSM)
* Regional, Multi*regional, Global
* Cloud KMS keys manged by FIPS 140*2 Level 3 certiifed HSMs
* Device hots encryption keys and performs cryptographic operations
* Enables you to meet complicance that mandates hardware environment
* Fully integrated with Cloud KMS
  * Same API, features, IAM integration
* Priced like Cloud KSM: active key versions sotres & key operations
  * But some key types more expensive: RSA, EC, long AES

Links:
* https://cloud.google.com/security*key*management


## Operations and Management
### Google StackDriver (like AWS Cloudwatch)
* Global
* Family or services for monitoring, logging & diagnosing apps on GCP/AWS/hybrid
* Service integrations add lots of values among Stackdriver and with GCP
* One Stackdriver account can track multiple:
  * GCP projects
  * AWS accounts
  * Other resources
* Simple usage*based princing
  * No longer previous systemn of tiers, allotments, and coverages


### StackDriver monitoring (like AWS Metrics & dashboards)
* Global
* Gives visibility into perf, uptime & overall health of cloud apps (based on collectd)
* Includes built*in/custom metrics, dashboards, global uptime monitoring & alerts
* Follow the trail: Links form alerts to dashboards/charts to logs to traces
* Cross*cloud: GCP, of course, but monitoring agent also support AWS
* Alert policy config includes multi*condition rules & resource organization
* Alert via email, GCP Mobile App, SMS, Slak, Pagerdutty, AWS SNS, etc
* automatic GCP/anthos metrics always free
* Pay for API calls & per MB for custom or AWS metrics


### StackDriver Logging (like AWS Cloudwatch Logs)
* Global
* Store, search, analyze, monitor, and alert on log data & events (based on Fluentd)
* Debug issues via integration with Stackdriver monitoring, Trace and error Reporting
* Create real*time metrics log data, then alert or chart them on dashboards
* Send real*time log data to BigQuery for avanced analytics and SQL*like querying
* Powerful interface to browse, search, and slice log data
* Export log data to GCS to cost*effectively store log archives


### StackDriver Error Reporting
* Global
* Counts, analyze, aggregates, and tracks crashes in helpul centralized interface
* Smartly aggregates errors into meaningful groups tailored to language/framework
* Instantly alerts when a new app error cannot be grouped with existing ones
* Link directrly form notifications to error details:
  * Time chart, occurrences, affected user count,  first/last seen dates, cleaned stack
* Exception stack trace parse knows JAva, python, javascript, ruby c, php and Go
* Jum form stack frames to source to start de debbuging
* No direct charge; py for source data in Stackdriver Logging


### StackDriver Trace (like AWS X*RAY)
* Global
* Tracks and display call tree & timing across distributed systems, to debug perf
* Automatically captures traces from Google App Engine
* Trace API and SDKs for Zipkin tracers to submit data to Stackdriver Trace
* View aggregate app latency info or dig into indivitdual traces to debug problems
* Generate reports on demand and get daily auto reports per traced app
* Detects app latency shift (degradation) over time by evaluating perf reports
* pay for ingesting and retrieving trace spans

### Stackdriver Debugger
* Global
* Grabs program state (callstack, variables, expressions) in live deploys; low impact
* logpoints repeat for up to 24h, fuller snapshots run once but can be conditional
* Source view supports Cloud Source Repository, Github, Bitbucket, local and upload
* JAva and python supported on GCE, GKE and GAE (standard and flex)
* node.js and ruby supported on GCE, GKE and GAE Flex; Go only on GCE and GKE
* Automatically enabled for GAE apps, agents avilable for others
* Share debbuging sessions with others (just send URL)


### StackDriver Profiler
* Global
* Continuous CPU and memory profillin to improve perf & reduce cost
* Low overhead (Typical: 0.5%; Max 5%) so use it in prod, too!
* supports Go, Java, Node, and python
* agent*based
* saves profiles for 30 days
* can download profiels for longer*team storage
* free to use


### Cloud Deployment manager (like AWS Cloudformation)
* Global
* Create/manage resources via declarative templates: Infrastructure as Code
* Declarative allow automaic parallelitzation
* templates writtent in YAML, python or Jinja2
* Supports input and output parameters, with json schema
* create and update of deployments both support preview
* free service; just pay for resources involved in deployments


### Cloud Billing API ((like AWS BIlling API)
* Global
* Programmatically manage billing for GCP projects and get GCP pricing
* Billing config
  * List billing accounts; get details and associated projects for each
  * Enable (associate), disable (disassociate), or change projects billing account
* Pricing
  * list billable SKUs; get public pricing (include tiers) for each
  * Get SKU metadata like regional availability
* Export of current bill to GCS or BQ is possible  but configured via console, not API


Links:
* https://cloud.google.com/billing/docs/
* https://cloud.google.com/deployment*manager/
* https://cloud.google.com/profiler/
* https://cloud.google.com/debugger/
* https://cloud.google.com/trace/
* https://cloud.google.com/error*reporting/
* https://cloud.google.com/logging/
* https://cloud.google.com/monitoring/
* https://cloud.google.com/products/operations


## Development and APIs
### Cloud Source Repositories (like AWS CodeCommit)
* Global
* Hosted private git respositories, with integration to GCP and other hosted repos
* Supports standard Git functionality
* no enhanced workflow support like pull requests
* can set up automatic sync form Github or Bitbucket
* natural integration with stackdriver debugger for live*debuggind deployed apps
* pay per project*user acitve each month (not prorated)
* pa per gb*month of data storage (prorated)
* pay per GB of data egress

### Cloud Build (like AWS CodeBuild)
* Global
* Continuously takes source code and builds, test and deploys it CI/CD service
* trigger from Cloud Source Repository (by branch, tag , or commit) or zip in GCS
  * can trigger form github and bitbucket via cloud source repositories reposync
* run many builds in parallel (currently at a time)
* dockerfile: super*simple build+push, plus scans for package vulnerabilities
* json/yaml file: flexible and parallel steps
* push or GCR and export artifacts to GCS * or anywhere your build steps write
* maintains build logs and build history
* pay per minute of build time * but free tier is 120 minutes per day


### Container Registry (GCR) (like Amazon ECR)
* Regional or multi*regional
* Fast, private docker image storage (based on GCS) with docker V2 registry API
* creates and manages and multi*regional GCS bucket, then trasnlates GCR calls to GCS
* IAM integration simplifies builds and deployments within GCP
* Quick deploys because of GCP networking to GCS
* Directly compatible with standard Docker CLI; native Docker login support
* UX integrated with Cloud Build and Stackdriver Logs
* UI to manage tags and search for images
* Pay directly for storage and egress of underlying GCS (no everhead)


### Cloud Enpoints (AWS Gateway)
* Global
* Handles authorization, monitoring, logging and API Keys for APIS backed by GCP
* Proxy instances are distributed and hook into Cloud Load Balancer
* Super*fast Extensible SErvice Proxy (ESP) container based on nginx: <1 ms/call
* uses JWTs and integrates with firebase, auth0, and google auth
* integrates with Stackdriver logging and Stackdriver Trace
* extensible service proxy (ESP) can transcode HTTP/JSON to gRPC
  * But API needs to be resource*orientd 
* pay per call to your API


### Apigee API Platform (like AWS API Gateway)
* Global
* full*featured and enterprise*scale API management platform for whole API lifecycle
* transform calls between diferent protocols: SOAP, REST, XML, binary, custom
* authenticate via OAuth/SAML/LDAP; authorize via Role*Based Access Control
* Thorttle traffic with quotas, manage API versions, etc
* Apigee Sense identifies and alerts administrators to suspicious API behaviors
* Apigee API Monetization supports various revenue models / rate pans
* team and bussiness tiers ar flat monthly rate with API call quotas and feature sets
* Enterprise tier and special feature pricing are Contact Sales


### Test Lab for Android (like AWS Device Farm)
* Global
* Cloud infrastructure for running test matrix cross variety of real Android devices
* Production*grade devices flashed with Android version and locale you specify
* robo test captures log files, saves annotated screenshots and video to show steps
  * defaul completely automatic but still deterministic, so can show regressions
  * can record custom script
* can also run Espresso and UI Automator 2.0 instrumentations tests
* firebase Spark and Flame plans have daily allotment of physical and virtual tests
* Blaze (PAYG) plan charges per device*hour * much less for virtual devices


Links:
* https://firebase.google.com/docs/test*lab/
* https://cloud.google.com/apigee
* https://cloud.google.com/endpoints/docs/grpc/transcoding
* https://cloud.google.com/endpoints/docs/openapi/architecture*overview
* https://cloud.google.com/endpoints/
* https://cloud.google.com/container*registry/
* https://cloud.google.com/cloud*build/
* https://cloud.google.com/source*repositories/