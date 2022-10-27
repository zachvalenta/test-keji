# TODO

## 参考

🗄 `distributed.md`

## current

## queue

https://github.com/PaulleDemon/AWS-deployment

overviews
* AWS https://softwareengineeringdaily.com/2021/06/07/aws-with-pete-cheslock/
* Azure https://softwareengineeringdaily.com/2021/06/08/azure-with-troy-hunt/
* GCP https://softwareengineeringdaily.com/2021/06/09/gcp-with-liz-fong-jones/
* Digital Ocean https://softwareengineeringdaily.com/2021/06/10/digital-ocean-with-john-allspaw/

Oblique API - hosting, CDN 🗄 hosting `system.md` proxy
* https://dev.to/harri_etty/the-introduction-to-servers-i-wish-i-d-had-44jl
* _level 2 (resellers)_: Heroku, Netlify, Render https://render.com/ https://softwareengineeringdaily.com/2019/06/17/render-high-level-cloud-with-anurag-goel/ Serverless https://serverless.com/
* _alternatives_: Platform.sh https://news.ycombinator.com/item?id=22486031, Zeit/Vercel https://news.ycombinator.com/item?id=22933479 OpenShift (RHEL managed Kubernetes https://news.ycombinator.com/item?id=3003289) Cloud Run https://alexolivier.me/posts/deploy-container-stateless-cheap-google-cloud-run-serverless Dokku http://dokku.viewdocs.io/dokku/ Cap Rover https://news.ycombinator.com/item?id=23465087 https://fly.io/
* _Digital Ocean_: https://github.com/seven1m/do-install-button

tighten perms for S3 buckets
* domains: www.zjayv.com, zjayv.com, zvtest1234
* yolo perms I used at the time
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::zjayv.com/*"
    }
  ]
}
```

## done

* _20_: Heroku (simple Django app)
* _18_: Cloud Foundry (Dark Canary)
* _17_: try out Terraform and AWS for Comcast interview

# AWS

⛩ https://console.aws.amazon.com/console/home
🔍 https://www.expeditedssl.com/aws-in-plain-english
📜
* https://aws.amazon.com/documentation/
* https://github.com/awsdocs
📚
* https://github.com/open-guides/og-aws
* https://www.lastweekinaws.com/

CLI
* access key: public key 💻 `~/.aws/config`
* secret access key: private key
* set
```sh
aws configure  # ~/.aws/config
```

compute
* spot instances: https://blog.codepen.io/2016/03/08/080-spot-instances/
* _Compute Engine_: EC2; compare prices https://ec2.shop/
* _ECS_ https://www.youtube.com/watch?v=I9VAMGEjW-Q
* _Fargate_: one level up from ECS
* _EMR_: Spark

za
* _Elastic Beanstalk_: PaaS (replaced by CodeStar?); apparently Beanstalk and Lightsail are not good https://softwareengineeringdaily.com/2019/06/17/render-high-level-cloud-with-anurag-goel/ 27:30 https://testdriven.io/blog/flask-elastic-beanstalk/
* _KMS_: password vault
* _SES_: email https://testdriven.io/blog/sending-confirmation-emails-with-flask-rq-and-ses/
* _CloudFormation_: deployment
* _CloudWatch_: monitoring if->then
* e.g. if Lambda throws error then raise alarm https://www.youtube.com/watch?v=lHWrAAzoxJA
* e.g. if ECS Kafka consumer writes log then forward to Datadog

queue
* _SNS_: pub sub 🔗 `amqp.md`
* _SQS_: queue

VPC
* _security group_: firewall; whitelist IPs your services can connect to (and vice versa) https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html
* https://www.verypossible.com/blog/aws-development-dark-art-of-vpc-networking
* https://dev.to/davidk01/aws-and-gcp-networking-differences-1fb1 https://twitter.com/paulg/status/1408442886023176198

certifications
* associate certs are easy but professional certs garner respect https://news.ycombinator.com/item?id=12198316 https://news.ycombinator.com/item?id=27580134
* Solutions Architect Associate https://www.freecodecamp.org/news/pass-the-aws-developer-associate-exam-with-this-free-16-hour-course/ https://aws.amazon.com/certification/certified-solutions-architect-associate/
* MIE https://news.ycombinator.com/item?id=29984721

clients
* _CLI_:  `~/.aws/config` https://github.com/awslabs/aws-shell https://github.com/donnemartin/saws https://realpython.com/python-boto3-aws-s3/ 🔗 `python.md` 'globals'
* run shell in browser https://aws.amazon.com/blogs/aws/aws-cloudshell-command-line-access-to-aws-resources/

za
* AWS is more expensive https://calpaterson.com/amazon-premium.html
* _benefits_: cost (sometimes) scalability (most times) geographic DR (nearly always)
* _clean up old resources_: https://github.com/genevieve/leftovers https://github.com/rebuy-de/aws-nuke https://github.com/servian/aws-auto-cleanup https://github.com/gruntwork-io/cloud-nuke
* _consultants_: https://aws.amazon.com/iq/ https://www.gruntwork.io/
* _cost control_: https://aws.amazon.com/aws-cost-management/aws-cost-explorer/ https://www.lastweekinaws.com/ https://github.com/mlabouardy/komiser
* _local dev_: https://github.com/localstack/localstack
* list resources https://github.com/jckuester/awsls
* _region_: collection of AZ http://cloudping.bastionhost.org/en/ https://status.aws.amazon.com/
* _scaling_: ElasticBeanstalk (autoconf mem) IaaS (set CloudWatch alert for cluster and add instances behind LB when load triggers alert)
* _security_: https://github.com/avishayil/caponeme
* _X-Ray_: trace HTTP req through n services https://www.freecodecamp.org/news/pass-the-aws-developer-associate-exam-with-this-free-16-hour-course/
* _sink_: https://twitter.com/dvassallo/status/1154516910265884672 https://www.aws.training/LearningLibrary https://acloud.guru/ https://www.reddit.com/r/aws/comments/aa7v1p/is_it_just_me_or_is_aws_is_a_nightmare_for/ https://cloudonaut.io/my-mental-model-of-aws/ http://blog.cleverelephant.ca/2019/07/aws-aurora.html?ck_subscriber_id=512830619 https://bravenewgeek.com/multi-cloud-is-a-trap/  https://github.com/jessebye/awser

## IAM

* rotate access key https://github.com/Fullscreen/aws-rotate-key
* https://learn.hashicorp.com/terraform/aws/iam-policy
* everthing is: _user_ (operator w/ permanent credentials; has API _access keys_ ID/secret) _group_ (collection of users) _role_ (user w/ tmp credentials) _policy_ (perms to access service; resource [S3] action [read] effect[boo]) https://stackoverflow.com/a/51888634/6813490
> Hal_9000 (_user_) is a computer_overlord (_role_) who can open_pod_bay_door (_policy_) and turn_off_life_support (_policy_).
* https://github.com/Netflix/repokid
* users default principal of least-permission
* create admin account and use that instead of root; it's root and then everyone else https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html
* handling keypairs https://www.tastycidr.net/using-aws-vault-with-linux
* give someone scoped access to account https://kevinslin.com/aws/aws_account_access_policies

## Lambda

* _alternatives_: Zappa https://www.youtube.com/watch?v=Vl5wroVmSuk https://www.reddit.com/r/django/comments/psddt8/zappa_is_no_longer_maintained/ w/ db https://romandc.com/zappa-django-guide/
* _blueprint_: bootstrap e.g. canary (cron to hit site)
* _debug_: get function running in EC2 (uses the same AMZ Linux AMI)
* _dependencies_: must be less than 250MB (uncompressed) and 50MB (compressed)
* frameworks Sparta (Golang) Chalice (Python)
* _internals_: https://brandur.org/go-lambda
* _perms_: necessar for the other services you're integrating with
* _runtimes_: need custom for something like jq https://docs.aws.amazon.com/lambda/latest/dg/runtimes-custom.html
* _startup time_: can reuse the container the function runs in https://medium.com/capital-one-tech/best-practices-for-aws-lambda-container-reuse-6ec45c74b67e
* _Step Functions_: flowchart for Lambda
* _time limit_: 300 sec; workaround is chaining functions and using something else (S3) to persist in the meantime

## messaging

* _MSK (Managed Streaming Kafka)_: take away operations overhead of running Kafka
* don't need to worry about patching infra, storage performance, monitoring replication across AZ https://www.youtube.com/watch?v=5yMzTwumD_g 3:20
* can also manual deploy Kafka https://aws.amazon.com/blogs/big-data/best-practices-for-running-apache-kafka-on-aws/
* _Eventbridge_: route events btw AWS services https://cloudonaut.io/versus/messaging/eventbridge-vs-msk/
* _Kinesis_: AWS version of Kafka https://engineering.statefarm.com/blog/comparison-of-aws-services-for-event-driven-architecture/
* _SQS_: API-based queue - you publish to an SQS queue and you consume from the queue https://stackoverflow.com/a/60543786

| factor             | MSK             | Eventbridge   |
|--------------------|-----------------|---------------|
| pricing            | per broker      | per msg       |
| protocol           | Kafka           | REST          |
| persistance        | forever         | awhile        |
| delivery guarantee | can config      | at least once |
| integrations       | Lambda          | all AWS       |
| encryption         | rest, transit   | rest, transit |

## network

network
* _ACM_: certificates
* _CloudFront_: CDN https://alexkudlick.com/blog/ila-cloudfront/index.html

----

* https://grahamlyons.com/article/everything-you-need-to-know-about-networking-on-aws

Route53
* = DNS
* https://stackoverflow.com/questions/51452111
* https://github.com/cloudkj/scar

__setup Route 53 as DNS service__: copy zone file to AWS, copy DNS info from AWS to DNS provider
* add zone file
```
Error parsing zone file: Error in line 1: no owner (encountered after 0 correct records) In line: @ 3601 IN SOA parkingpage.namecheap.com.
```
* add `$origin example.com.` to first line 
https://ubuntuforums.org/showthread.php?t=1216801 
https://hathaway.cc/2011/02/how-to-import-bind-zone-files-into-amazon-route-53/
```
Error parsing zone file: Unsupported directive: $origin
```
* add `@origin example.com.` to first line http://shon.github.io/2014/12/21/dns_migration_story.html
```
Error parsing zone file: Error in line 1: Invalid type 'example.com.' (encountered after 0 correct records) In line:@origin example.com.
```
* add `$ORIGIN www.zjayv.com` to first line, rm white space from each line --> WORKS!

__other options if that doesn't work__ 
* remove white space from beginning of each line
* add TTL thing to second line
* try cli53
* ask Stack Overflow

https://www.youtube.com/watch?v=W4FPZ29Trpw
https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/migrate-dns-domain-inactive.html
https://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html
http://shon.github.io/2014/12/21/dns_migration_story.html
http://blog.alfredcalayag.com/development/2015/03/02/personal-site-hosted.html
https://www.youtube.com/watch?v=D6qB7MEFOe0

## storage

db https://www.lastweekinaws.com/blog/running-relational-databases-on-aws/
* _neon_: https://neon.tech/ https://news.ycombinator.com/item?id=31536827
* _Aurora_: dbms; can migrate from/to MySQL/Postgres; fastest growing service
* _DMS_: db migrations
* _DynamoDB_: NoSQL https://www.freecodecamp.org/news/ultimate-dynamodb-2020-cheatsheet/
* _RDS_: DBaaS; supports Aurora + others; under the covers is just dmbs on top of EC2 but w/ backups/updates for free (vs. doing yourself)
* _Redshift_: analytics for big data; have to manage
* _Athena_: BigQuery w/ S3 as datastore

file
* _block_: mount to instance, 1 clients; EBS can be snapshot, instance volume is default and temporary
* _file_: mount to instance, n clients
* _object_: don't mount to instance, used by n clients
* _EBS_: attachable storage for EC2; can be snapshot
* _EFS_: like S3 but mimics filesystem (slower bc file locked over wire vs. OS calls) https://blog.codepen.io/2017/05/09/129-projects-infrastructure/
* _Glacier_: S3 but cheaper in exchange for higher latency
* _S3_: obj storage
* Python driver https://github.com/Miserlou/NoDB
* https://news.ycombinator.com/item?id=30371604
* can take 0.5 million RPS https://www.dataengineeringpodcast.com/upsolver-data-lake-database-administrator-episode-135/ 13:30
* https://tech.marksblogg.com/minio-aws-s3-hdfs.html

# CONFIG MGMT

config mgmt in general
* _config mgmt_: provision server remotely
* SQL https://news.ycombinator.com/item?id=28554089
* _other tools_: Ansible-like (Puppet, Chef, Salt) https://github.com/Fizzadar/pyinfra https://www.pythonpodcast.com/pyinfra-configuration-management-episode-270/ http://scriptedconfiguration.org/

remote execution
* subprocess, sultan
* _Paramiko_: https://github.com/paramiko/paramiko
* _Fabric_: execute script on server; apparently not meant for fully-fledged config mgmt https://stackoverflow.com/questions/39370364/when-to-use-fabric-or-ansible but can/could be used with Ansible (article doesn't explain why not just use Ansible and is undated)

## Ansible

🗄 `system.md` config
🧪 https://github.com/zachvalenta/ansible-hello-word-macos
📺
* https://www.youtube.com/playlist?list=PL2_OBreMn7FqZkvMYt6ATmgC0KAGGJNAN
* https://www.ansiblefordevops.com/
* https://serversforhackers.com/s/ansible

semantics
* _control_: controls execution
* needs Linux, Python https://docs.ansible.com/ansible/latest/dev_guide/developing_locally.html#modules-and-plugins-what-s-the-difference
* _worker_: SSH into remote and run plays for control node
* _target_: runs plays
* agentless i.e. don't need anything Ansible-related installed
* _Tower_: PaaS layer (perms, credentials, notifications, scheduling, API, reporting); makes secrets easy, just encrypt using Tower and then you can store encrypted secrets files in your repo and when playbooks in repo run by Tower it will use private key to decrypt (assume it figures out which pk to use via repo/project metadata referenced when encrypting)
* _inventory_: list of all remotes
* _play_: task (install app, start service)
* _playbook_: list of plays; linter https://github.com/ansible/ansible-lint `ansible-playbook -c local` run playbook in cwd and run against localhost ❓ `-i` in Ryan's Makefile
* _plugin_: extends Ansible, executes on control node https://docs.ansible.com/ansible/latest/dev_guide/developing_locally.html#modules-and-plugins-what-s-the-difference
* _module_: impl of play, executes on target node; e.g. `ansible -m setup`; BYO https://www.youtube.com/watch?v=nyXDR4RG4A8

todo
* go through https://github.com/KeyboardInterrupt/awesome-ansible
* _infra for testing_: why use Vagrant? possible to use Docker? can you follow his course just using localhost? https://www.youtube.com/watch?v=goclfp6a2IQ
* _with other tools_: why use Ansible with Terraform? https://www.youtube.com/watch?v=-gKTeT3BgHE https://www.hashicorp.com/resources/ansible-terraform-better-together https://github.com/adammck/terraform-inventory Fabric https://realpython.com/automating-django-deployments-with-fabric-and-ansible

inventory
* will use from cwd if present and otherwise fall back to
* fmt: can be INI or YAML https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#inventory-basics-formats-hosts-and-groups 
* create groups https://buildvirtual.net/creating-a-simple-ansible-playbook/

config
* _config_: tells you where inventory is
* _locations_: installed via pipx so just using config per project for now https://stackoverflow.com/q/21958727 https://raw.githubusercontent.com/ansible/ansible/devel/examples/ansible.cfg
* Pyhton interpreter https://docs.ansible.com/ansible/latest/reference_appendices/interpreter_discovery.html

plugins 
* docs https://docs.ansible.com/ansible/latest/plugins/plugins.html
* output https://www.youtube.com/watch?v=VfrSCz_5yjg https://github.com/dodevops/ansible-teamcity-callback https://www.jeffgeerling.com/blog/2018/use-ansibles-yaml-callback-plugin-better-cli-experience
* post https://stackoverflow.com/questions/30509058/post-json-to-api-via-ansible
* _conf_: in ansible.cfg? https://github.com/search?p=5&q=callback_whitelist+filename%3Aansible.cfg&type=Code https://termlen0.github.io/2019/11/16/observations/
```conf
# pass args
[ur_plugin]
team = foo_team
```
```py
# map args to Python module's namespace

# reference
```

```conf
[defaults]
inventory      = ~/Desktop/proj/inventory.yml
```

run locally
* local_action https://www.educba.com/ansible-local_action/
* from playbook, from shell https://www.shellhacks.com/ansible-localhost-run-playbook-locally-local-command/ https://www.middlewareinventory.com/blog/run-ansible-playbook-locally/
* all options, best practices https://gist.github.com/alces/caa3e7e5f46f9595f715f0f55eef65c1
* specify inventory from config https://www.rogerperkin.co.uk/network-automation/ansible/inventory-file/
```yml
localhost              ansible_connection=local
```
```sh
$ ansible -m ping all
localhost | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```

## Terraform

* CLI to query https://github.com/mazen160/tfquery
* Python alternative https://www.pulumi.com/ https://leebriggs.co.uk/
* security scan https://github.com/tfsec/tfsec
* get cost estimate https://www.infracost.io/
* use languages other than HCL https://www.terraform.io/cdktf https://www.thoughtworks.com/radar/tools?blipid=202203047
* test config https://github.com/open-policy-agent/conftest https://www.thoughtworks.com/radar/tools?blipid=202110014

---

📜 [ur-list](https://github.com/shuaibiyy/awesome-terraform)

* _sink_: https://grahamlyons.com/article/a-zero-fricton-terraform-primer
* _install_: spring 2019 tried to use Homebrew but no luck (`tf-brew.log`), then seemed like I downloaded binary into project folder (`/Users/zach/Desktop/home/kaifa/SDLC/6_IaC/terraform`), then created symlink in `usb/bin` (using `sudo`!?!), which I presume is no longer there as a result of upgrading to Mojave (`installs/terraform/tf-path.log`), I still had the binary lying around inside `assets-digital/installs/terraform` but deleted it -> official docs and [some tutorials](https://grahamlyons.com/article/a-zero-fricton-terraform-primer) say to install binary, [others to use Homebrew](https://developers.cloudflare.com/terraform/getting-started/installing/) and Bellavance does mention using Chocolatey, I tried Homebrew

what TF does
> generates a dependency graph of the resources and, when run against one or more providers, walks that graph and ensures that the resources exist and are configured as defined
* dependency graph https://medium.com/doctrine/scaling-our-dependency-graph-7ab42b640286

how to use IRL
> We have a strict policy where everything (creating, updating or deleting) should be done through Terraform and the AWS console should be used as a read-only dashboard...We have alerting setup for any action that is performed in our AWS accounts that was done through the console...we're looking to move to an automated environment such as Atlantis or Terraform Enterprise later this year. + how to keep everything in sync https://news.ycombinator.com/item?id=19360031

* _components_: runtime + config (`.tf`) + storage (`.tfstate`) + secrets (`.tfvars` w/ `-var-file=path`)
* _variables_: types (string, list, map) precedence (CLI > file > hard-coded)

directory structure
```sh
├── dir
│   └── my_conf.tf  # tf cmd will include any .tf files in $CWD unless `.ignore` extension
│   └── terraform.state  # locked when in use, need to store in repo
```

* keeps track of state via `.tfstate`, can also refresh from provider, looks at state then config and then says "right, what do I need to do to state to make it like the dependency graph I've generated from the config file?"
* generate config from existing AWS resources https://former2.com/

commands
* _terraform_: help
* _init_: install plug-in for provider into `.terraform` in `$CWD`
* _plan_: generate dependency graph for resources
* _apply_: `plan` + deploy
* _destroy_: preview w/ `plan -destroy`

config
* _variable_: data
* _provider_: AWS, Azure, et al.; BYO https://vincent.composieux.fr/article/create-a-provider-plugin-for-terraform/
* _resource_: EC2, S3, et al. + _provisioner_ (code block to do something to resource)
* _output_: pipe elsewhere

terms
* _provider_: AWS, Azure, et al.
* _resource_: provider's infra
* _variable_: your data
* _data_: provider data
* _output_: attributes provider gives back

# QUEUES

## Kafka

🗄 `db.md` data eng
📜 https://kafka.apache.org/documentation/
📙 Narkhede guide
📹
* 101 https://www.youtube.com/playlist?list=PLa7VYi0yPIH0KbnJQcMv5N9iW8HkZHztH
* talk https://www.youtube.com/watch?v=Ltgt0ekso4c
* example https://www.youtube.com/channel/UCDankIVMXJEkhtjv5yLSN4g/videos

run
* Docker https://www.youtube.com/watch?v=qi7uR3ItaOY 4:00
* GUIs https://news.ycombinator.com/item?id=24099037 https://akhq.io/
* alternative https://github.com/liftbridge-io/liftbridge
* no more Zookeeper (impl yet?) https://news.ycombinator.com/item?id=23207377 https://www.confluent.io/blog/kafka-without-zookeeper-a-sneak-peek/
* _Confluent_: managed Kafka https://news.ycombinator.com/item?id=26644713

semantics
* _topic_: group of msgs
* can have n consumers for 1 topic
* _producer_: write msg to topic
* _consumer_: read msg from topic
* read doesn't destroy msg (unlike MQ)
* can either stream or batch https://kafka.apache.org/intro.html

usage
* as distributed commit log https://news.ycombinator.com/item?id=26644713
> same as audit log?

protocol https://kafka.apache.org/0100/protocol.html
* rides on top of TCP so you need client per language https://strimzi.io/blog/2019/07/19/http-bridge-intro/
* handshake https://pierrezemb.fr/posts/diving-into-kafka-protocol/
* _message set_: msgs grouped https://kafka.apache.org/documentation/#maximizingefficiency

alternatives
* _AWS SQS_: https://cheesecakelabs.com/blog/asynchronous-task-queue-django-celery-aws-sqs
* _Pulsar_: Kafka alternative
* _Rabbit_: comes w/ own db https://stackoverflow.com/q/38444425
* vs. Kafka https://aws.amazon.com/msk/what-is-kafka/
* _ZeroMQ_: http://aosabook.org/en/zeromq.html

za
* streaming architecture https://news.ycombinator.com/item?id=31421004
* BYO https://github.com/travisjeffery/jocko
* https://developer.confluent.io/what-is-apache-kafka/#intro-to-ak
* https://www.confluent.io/blog/author/martin-kleppmann/
* Avro (eventbus README)
* https://unitedmasters.atlassian.net/wiki/spaces/ENG/pages/322273452/Event+Bus+System

## Rabbit

* _attributes - queue_: durability (keep in mem, write to disk, write to db bc broker can restart, fail) time-to-live (how long to keep in the queue?) security (what consumers have access?) batching (delivery immediately or wait until x messages before allowing consumers to take)
* _attributes - message_: id, user/groups id, creation time, reply to, subject https://www.rabbitmq.com/tutorials/amqp-concepts.html
* _AMQP_: protocol for MQ; alternatives incl. JMS, MSMQ, STOMP (text vs. binary for AMQP); originated in 2003 at JP Morgan, worked w/ Red Hat to create Qpid; can set version in HTTP but not AMQP https://www.digitalocean.com/community/tutorials/an-advanced-message-queuing-protocol-amqp-walkthrough
> Unlike JMS, which defines an API and a set of behaviors that a messaging implementation must provide, AMQP is a wire-level protocol. A wire-level protocol is a description of the format of the data that is sent across the network as a stream of bytes. Consequently, any tool that can create and interpret messages that conform to this data format can interoperate with any other compliant tool irrespective of implementation language. - https://spring.io/understanding/AMQP
* _consumer ack_: queue only rm msgs when consumer acks https://www.rabbitmq.com/tutorials/amqp-concepts.html
* _consumer priority_: defaults to highest in Qpid https://qpid.apache.org/releases/qpid-broker-j-7.0.6/book/Java-Broker-Runtime-Consumers.html#Java-Broker-Runtime-Consumers-Prioirty Spring allows setting on the consumer side but JMS doesn't https://stackoverflow.com/q/53602831/6813490 https://docs.spring.io/spring-amqp/reference/htmlsingle/#consumer-priority but does allow message priority https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jms/core/JmsTemplate.html#setPriority-int-
* _back pressure_: pressure from data source to write new data when streaming system is already holding too much (e.g. bc consumer hasn't ingested) [Macey 39:00]
* _order_: round robin in RabbitMQ https://www.rabbitmq.com/consumer-priority.html

semantics
* _entity_: producer, consumer
* _broker(queue)_: app to send/rec/store msgs conforming to AMQP
* _exchange_: receives message, routes to queue
* _queue_: entity that holds msg for consumer
* _binding_: rule for routing from exchange to queue
* _entity_: collective name for queue, exchange, binding https://www.rabbitmq.com/tutorials/amqp-concepts.html
* used to offload long-running operations outside HTTP req-res cycle options (email, report generation, talking to third-party services) https://nickjanetakis.com/blog/4-use-cases-for-when-to-use-celery-in-a-flask-application
* don't need presently available connection (unlike API) https://www.netlify.com/blog/2017/03/02/to-message-bus-or-not-distributed-systems-design/
* use for all db operations?!? https://www.openmymind.net/Grow-Up-Use-Queues/
* https://news.ycombinator.com/item?id=22901856 Kleppmann 4.136

## task

🗄 `shell.md` jobs
🛠 https://taskqueues.com/

Celery
* Redis as db for Celery jobs https://ljvmiranda921.github.io/notebook/2019/11/08/flask-redis-celery-mcdo/
* _Flower_: monitor Celery https://testdriven.io/blog/flower-nginx/
*  https://www.agiliq.com/blog/2015/07/getting-started-with-celery-and-redis/
*  https://djangostars.com/blog/the-python-celery-cookbook-small-tool-big-possibilities/
*  https://testdriven.io/blog/asynchronous-tasks-with-falcon-and-celery/
*  https://adamj.eu/tech/2020/02/03/common-celery-issues-on-django-projects
*  https://stackshare.io/sentry/how-sentry-receives-20-billion-events-per-month-while-preparing-to-handle-twice-that
*  https://nickjanetakis.com/blog/4-use-cases-for-when-to-use-celery-in-a-flask-application

Redis Queue (RQ)
* https://testdriven.io/blog/asynchronous-tasks-with-flask-and-redis-queue/
* https://pyvideo.org/pygotham-2018/tracking-the-international-space-station-in-django-with-redis-queue-and-rq-scheduler.html
* https://testdriven.io/blog/sending-confirmation-emails-with-flask-rq-and-ses/#workflow
* https://testdriven.io/blog/developing-an-asynchronous-task-queue-in-python/

alternatives
* _Django Q_: uses Django's own db to store tasks https://www.valentinog.com/blog/django-q https://django-simple-task.readthedocs.io
* _Huey_: https://www.untangled.dev/2020/07/01/huey-minimal-task-queue-django https://runninginproduction.com/podcast/4-real-python-is-one-of-the-largest-python-learning-platforms-around#27:00 https://github.com/coleifer/huey
* Postgres https://github.com/procrastinate-org/procrastinate

# SERVERS

* benchmark: https://github.com/wg/wrk https://github.com/giltene/wrk2 https://github.com/rakyll/hey https://github.com/encode/starlette#performance https://falconframework.org/#sectionBenchmarks https://www.webpagetest.org/
* mock server: https://smocker.dev/
* URL for dev server: ngrok
* _Apache_: on start, Apache runs as master process `root` and binds to port 80; pre-fork (master process spawns child proccesses under UID `apached` to wait for connections) https://stackoverflow.com/a/25894770/6813490
* _CGI_: process per req (vs. connection) cannot keep db connection over multiple
* https://justine.lol/redbean/index.html https://news.ycombinator.com/item?id=27431910 https://news.ycombinator.com/item?id=27434494
* comment server: Disqus, isso https://avi.im/blag/about/ https://posativ.org/isso/docs/

## Caddy

📜 https://github.com/caddyserver/caddy

do these next https://caddyserver.com/docs/getting-started https://caddyserver.com/docs/quick-starts

* license https://news.ycombinator.com/item?id=24434709
* _design_: no dependencies (not even libc); modules impl in Go
* _config_: via file or API

---

* _install_: macOS (Homebrew) other UNIX https://nginx.org/en/linux_packages.html
* _functionality_: caching https://danielmiessler.com/blog/nginx-caching-tempfs/ https://serversforhackers.com/c/nginx-caching rate limiting https://lincolnloop.com/blog/rate-limiting-nginx/ TLS https://raymii.org/s/tutorials/Strong_SSL_Security_On_nginx.html https://botleg.com/stories/https-with-lets-encrypt-and-nginx/
* _monitoring_: https://github.com/lebinh/ngxtop https://www.scalyr.com/community/guides/how-to-monitor-nginx-the-essential-guide https://www.honeycomb.io/blog/tell-me-more-nginx/ https://news.ycombinator.com/item?id=23466506
* _processes_: master (read config, manages workers) workers (handles requests)
* _server block_: running more than one site on single host; 类似 Apache virtual host; done w/ `sites-enabled` `sites-available` `conf.d` (macOS only has `servers`) https://stackoverflow.com/a/41303948/6813490

cmds
* _start_: `nginx`
* _stop_: `-s quit` (will wait for workers serving req to finish)
* _reload conf_: `-s reload`

conf
* ❓ per-project config: server block? symlink?
* generate https://www.digitalocean.com/community/tools/nginx 
* security lint https://github.com/yandex/gixy 
* location (Linux `/etc/nginx/nginx.conf` macOS `/usr/local/etc/nginx/nginx.conf`) 
* language: Nginx's own thing despite looking like JSON https://carrot.is/coding/nginx_introduction

## Gunicorn

📜 https://docs.gunicorn.org/en/stable/

config
* some settings only available from file https://docs.gunicorn.org/en/latest/settings.html
* _Docker_: start 2 workers (avoid heartbeat time out and scheduler restarting container) conf file for heartbeat (use `/dev/shm`) https://pythonspeed.com/articles/gunicorn-in-docker/
* _precedence_: command line > file > defaults https://docs.gunicorn.org/en/stable/configure.html
* _daemon_: https://stackoverflow.com/a/30503078 https://stackoverflow.com/a/52824526 ❓ so far `--daemon` keeps it running even after terminal closes; thought that every process created from terminal/tty (what's the diff again?) is a subprocess of that terminal and thus stops when terminal closes; other options -> systemd https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-gunicorn-and-nginx-on-ubuntu-16-04 supervisord https://mattsegal.dev/simple-django-deployment.html https://stackoverflow.com/questions/24941791/starting-flask-server-in-background https://prakhar.me/articles/flask-on-nginx-and-gunicorn/ screen https://stackoverflow.com/a/2975657/6813490 https://www.digitalocean.com/community/questions/how-keep-my-app-running-after-close-putty-f82aab17-ca84-46a0-8a39-3e25f1dd2d45

* command line
```sh
# Flask
gunicorn app:app  # defaults to localhost on port 8000 
gunicorn -b 127.0.0.1:5999 app:app  # specify port
gunicorn -b 0.0.0.0:5999 app:app  # take req from outside os
gunicorn -b 0.0.0.0:5999 app:app --daemon  # run in background

# Django https://docs.djangoproject.com/en/3.0/howto/deployment/wsgi/gunicorn/
gunicorn project.wsgi  # locahost
gunicorn project.wsgi -c guni-conf.py  # run using config file
gunicorn -b 0.0.0.0:5999 project.wsgi  # take req from outside os
```
* file
```python
import os
from dotenv import load_dotenv, find_dotenv

load_dotenv(find_dotenv())
host = os.getenv("APP_HOST")
bind = f"{host}:8000"
accesslog = "-"
```

logging https://mattsegal.dev/django-gunicorn-nginx-logging.html
* _access log_: each req; write to stdout with `accesslog = "-"`
* _error log_: info on start up, shut down
* `caputure_output`: grab info emitted from Django logs and incl in gunicorn log output

design
* pre-fork
* _processes_: typically run different workers, each with their own process https://pythonspeed.com/articles/gunicorn-in-docker/
* works best w/ Nginx https://gunicorn.org/#deployment 
* does ASGI https://sanic.readthedocs.io/en/latest/sanic/deploying.html#running-via-gunicorn https://github.com/encode/starlette#performance

## Nginx

📜 https://nginx.org/en/docs/beginners_guide.html https://nginx.org/en/docs/ https://github.com/trimstray/nginx-admins-handbook

non-Docker
* https://stackoverflow.com/a/54298517
* https://mattsegal.dev/nginx-django-reverse-proxy-config.html
* https://github.com/zachvalenta/nginx-wsgi
* https://www.patricksoftwareblog.com/how-to-configure-nginx-for-a-flask-web-application/
* https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx
* https://www.youtube.com/watch?v=hxngRDmHTM0

Docker
* compose file https://www.youtube.com/watch?v=hxngRDmHTM0 https://pawamoy.github.io/posts/docker-compose-django-postgres-nginx/#compose-add-a-container-for-nginx https://github.com/pawamoy/docker-nginx-postgres-django-example/blob/master/config/nginx/conf.d/local.conf https://github.com/wiamsuri/django-gunicorn-nginx-docker/blob/master/docker-compose.yml
* separate Dockerfile https://www.codementor.io/@samueljames/nginx-setting-up-a-simple-proxy-server-using-docker-and-python-django-f7hy4e6jv https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/#nginx
* https://github.com/productive-dev/minimal-reverse-proxy-demo/blob/master/docker-compose.yml
* https://github.com/bunkerity/bunkerized-nginx

* example
```conf
# https://gunicorn.org/#deployment 

# things set here: log fmt, mime types, access log location https://www.patricksoftwareblog.com/how-to-configure-nginx-for-a-flask-web-application/
http {

    # servers for Nginx to balance btw https://www.youtube.com/watch?v=BRPvjNQsqis https://www.youtube.com/watch?v=spbkCihFpQ8 https://www.nginx.com/resources/wiki/start/topics/examples/loadbalanceexample/ https://nginx.org/en/docs/http/ngx_http_upstream_module.html
    upstream name_for_upstream {
        server localhost:8777;
        server localhost:8778;
    }

    server {
        listen 80;  # set port for Nginx itself
        server_name example.org;
        access_log  /var/log/nginx/example.log;

        # location = URL mapping
        location / {
            # pass requests here (assuming app running on same box)
            proxy_pass http://127.0.0.1:8000;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
        # serving static files
        location /static/ {
            # read from disk instead of passing req to WSGI server https://mattsegal.dev/nginx-django-reverse-proxy-config.html
            root /home/myuser/myproject;
        }
    }
}
```

config misc
* generator https://www.digitalocean.com/community/tools/nginx 
* linting https://github.com/yandex/gixy 
* file locations (Linux `/etc/nginx/nginx.conf` macOS `/usr/local/etc/nginx/nginx.conf`)

config syntax https://stackoverflow.com/a/46918583
* https://jvns.ca/blog/2021/09/24/new-tool--an-nginx-playground/
* syntax is custom, kinda looks like JSON, comments via hash at start of line https://unix.stackexchange.com/a/302823
* _directive_: name (mapping to Nginx module) that takes n params
* _simple directive_: one liner
* _block directive_: n lines; events (how many processes) http (routing) https://www.patricksoftwareblog.com/how-to-configure-nginx-for-a-flask-web-application/ aka 'context'
* _main_: anything outside block scope https://www.patricksoftwareblog.com/how-to-configure-nginx-for-a-flask-web-application/

misc
* scripting w/ Lua https://news.ycombinator.com/item?id=10618622
* cache to memory https://danielmiessler.com/blog/nginx-caching-tempfs/
* _docroot_: where Nginx finds files; `/usr/local/Cellar/nginx/1.15.7/html`
* _processes_: master (read config, manages workers) workers (handles requests)
* _server block_: running more than one site on single host; 类似 Apache virtual host; done w/ `sites-enabled` `sites-available` `conf.d` (macOS only has `servers`) https://stackoverflow.com/a/41303948/6813490
* seems like no one uses the commercial version https://dropbox.tech/infrastructure/how-we-migrated-dropbox-from-nginx-to-envoy

functionality and utils
* caching https://danielmiessler.com/blog/nginx-caching-tempfs/ https://serversforhackers.com/c/nginx-caching
* rate limiting https://lincolnloop.com/blog/rate-limiting-nginx/ https://preparingforcodinginterview.wordpress.com/2019/10/19/rate-limiting-algorithm-algo/
* TLS https://raymii.org/s/tutorials/Strong_SSL_Security_On_nginx.html https://botleg.com/stories/https-with-lets-encrypt-and-nginx/
* monitoring https://github.com/lebinh/ngxtop https://www.scalyr.com/community/guides/how-to-monitor-nginx-the-essential-guide https://www.honeycomb.io/blog/tell-me-more-nginx/ https://news.ycombinator.com/item?id=23466506

cmds
* _start_: `nginx`; starts as root and then switches to whatever user you config https://blog.bejarano.io/how-to-write-great-container-images/
* _stop_: `-s quit` (will wait for workers serving req to finish)
* _reload conf_: `-s reload`

## uWSGI

* run options https://blog.ionelmc.ro/2022/03/14/how-to-run-uwsgi/
* _docs_: good God; scroll past 42 changelogs for the README, and commercial support in Italian https://github.com/unbit/uwsgi-docs#commercial-support
* _multilanguage_: e.g. Ruby support, although have never heard of its usage outside Python

* install
* shell command https://github.com/zachvalenta/flask-skeleton/commit/435517e5e1353eaa875d16e91ea96e47300b35dc
```sh
# https://uwsgi-docs.readthedocs.io/en/latest/WSGIquickstart.html#deploy-it-on-http-port-9090
uwsgi --http :9090 --wsgi-file foobar.py

# https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uswgi-and-nginx-on-ubuntu-18-04
# https://github.com/zachvalenta/flask-uwsgi-scaffold
uwsgi --socket 0.0.0.0:8000 --protocol=http -w wsgi

# expects app obj to be named `application` https://riptutorial.com/flask/example/16286/using-uwsgi-to-run-a-flask-application
# rename w/ `callable` https://uwsgi-docs.readthedocs.io/en/latest/WSGIquickstart.html#deploying-flask
# https://uwsgi-docs.readthedocs.io/en/latest/WSGIquickstart.html#deploying-flask
uwsgi --http :5002 --wsgi-file app.py --callable app

# https://uwsgi-docs.readthedocs.io/en/latest/WSGIquickstart.html#adding-concurrency-and-monitoring
uwsgi --http :9090 --wsgi-file foobar.py --master --processes 4 --threads 2
uwsgi --http :9090 --wsgi-file foobar.py --master --processes 4 --threads 2 --stats 127.0.0.1:9191
```

* can also point to app obj via `uwsgi.py` or `uwsgi.ini` https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uwsgi-and-nginx-on-ubuntu-14-04 https://www.youtube.com/watch?v=lnFMKAIHRcA
```sh
uwsgi --socket 0.0.0.0:8000 --protocol=http -w wsgi --callable
```
```python
from myproject import application
if __name__ == "__main__":
    application.run()
```

# TELEMETRY

🗄 `distributed.md` tracing

* _alerts_: https://brandur.org/alerting notification fatigue (when alerts stop mattering)

* metrics, logs, traces https://opentelemetry.io/ https://github.blog/2021-05-26-why-and-how-github-is-adopting-opentelemetry/

semantics
* _metric_: frequency
* _log_: details
* specific
* _trace_: code path
* sampled

## analytics

> Then came the rise of real-time digital analytics. Every digital newsroom in the country, including Vox, subscribes to some service or another that tracks traffic in a gamified, constantly updating interface. The most influential is Chartbeat, which shows you every article on your site, indicates the number of people on each article at any given second, and colors the dots representing those people to tell you how they found the article. Green dots mean they found you through a search engine. Purple dots mean they came from a social network, usually Facebook, Twitter, or Reddit. It’s pure pleasure to watch the display for an article you worked hard on fill with dots. https://www.vox.com/2020/1/28/21077888/why-were-polarized-media-book-ezra-news

* _analytics_: aka customer data infra
* _clickstream_: series of links user follows or things they click on

* for CLI https://www.visidata.org/blog/2021/usage-graphs/
> build modern CLI applications without worrying about user accounts, data storage and encryption https://github.com/charmbracelet/charm#charm-kv
https://github.com/posthog/posthog
https://www.arp242.net/personal-analytics.html
https://uglyduck.ca/fathom-analytics-netlify/ https://uglyduck.ca/self-hosting-fathom/
https://news.ycombinator.com/item?id=26848827
https://news.ycombinator.com/item?id=26424855
https://news.ycombinator.com/item?id=25375148
https://softwareengineeringdaily.com/2020/07/01/snowplow-analytics-data-collection-platform-with-alex-dean/
https://softwareengineeringdaily.com/2020/11/02/hightouch-customer-data-warehouse/

observability: Datadog, Grafana, Prometheus
brew analytics https://docs.brew.sh/Analytics
Clickhouse https://news.ycombinator.com/item?id=24696149 https://tech.marksblogg.com/clickhouse-prometheus-grafana.html  https://softwareengineeringdaily.com/2021/05/17/clickhouse-data-warehousing-with-robert-hodges/

analytics
* https://www.goatcounter.com/ -> Visidata uses
* https://simpleanalytics.com/ https://newcss.net/
* https://plausible.io/privacy-focused-web-analytics https://www.erichgrunewald.com/posts/ravi-zacharias-solves-the-problem-of-evil/
* https://news.ycombinator.com/item?id=26379569
* https://plausible.io/self-hosted-web-analytics

* _segmented users_: when you care about individual user behavior i.e. they're paying; Mixpanel, Posthog https://www.pythonpodcast.com/posthog-product-analytics-episode-266/ 8:00
* _non-segmented users_: for media site where you don't care about an individual user's behavior; Google Analytics https://www.pythonpodcast.com/posthog-product-analytics-episode-266/ 8:00

* event collection https://github.com/ksensehq/eventnative
* _BYO_: https://www.pcmaffey.com/roll-your-own-analytics https://www.youtube.com/watch?v=SMRaHSZiwWE https://healeycodes.com/privacy-focused-analytics-from-scratch/
* _self-hosting_: https://news.ycombinator.com/item?id=24198329
* _options_: https://github.com/plausible/analytics https://benhoyt.com/writings/replacing-google-analytics/ https://usefathom.com/ https://minimalanalytics.com/ https://thomashunter.name/posts/2018-12-28-migrating-from-google-analytics https://simpleanalytics.io https://plausible.io/blog/remove-google-analytics https://github.com/milesmcc/shynet https://selfhostedsource.tech/category/self-hosted/analytics https://github.com/electerious/Ackee https://github.com/milesmcc/shynet https://blog.simpleanalytics.io/why-we-moved-our-servers-to-iceland https://github.com/PostHog/posthog https://news.ycombinator.com/item?id=22044876 https://matomo.org/ Segment https://news.ycombinator.com/item?id=24737244

* ❓ withoutba 'backend-only' = no tracking https://www.benkuhn.net/about/
* ❓ track visitors without using cookies necessary to avoid GDPR popup? https://marvinblum.de/blog/server-side-tracking-without-cookies-in-go-OxdzmGZ1Bl
* https://danluu.com/metrics-analytics/, GoatCounter, https://www.kalzumeus.com/greatest-hits/ https://danluu.com/web-bloat https://thoughtbot.com/upcase/analytics-for-developers 

## logging

🗄 `python.md` logging

---

* log to stdout https://www.youtube.com/watch?v=aQikNWEaJUQ
* https://blog.twitter.com/engineering/en_us/topics/infrastructure/2021/logging-at-twitter-updated
https://news.ycombinator.com/item?id=30394152
> If you are building an API, having a mechanism that provides detailed logs—including the POST bodies passed to the API—is invaluable. It’s an inexpensive way of maintaining a complete record of what happened with your application—invaluable for debugging, but also for tricks like replaying past API traffic against a new implementation under test. Logs like these may become infeasible at scale, but for a new project they’ll probably add up to just a few MBs a day—and they’re easy to prune or switch off later on if you need to. https://simonwillison.net/2021/Jul/1/pagnis/
* _Logflare_: middleman btw app and storage; most logging services (datadog) make money by marking up storage; available as Cloudflare app https://runninginproduction.com/podcast/11-logflare-is-a-log-management-and-event-analytics-platform
* _sources_: clickstream, proxy, web server, app server
* event streams https://apenwarr.ca/log/20190216
* _formats_: CLF, Amazon, Nginx https://github.com/allinurl/goaccess common log format https://vicki.substack.com/p/logs-were-our-lifeblood-now-theyre https://brandur.org/logfmt https://medium.com/hiredscore-engineering/logging-lets-do-it-right-41d568d3bfcd
* _trace id_: GUID attached to all related logs to track workflow
* _tools_: Logstash, Fluentd https://github.com/itamarst/eliot https://news.ycombinator.com/item?id=21461617 https://github.com/rcoh/angle-grinder https://github.com/trimstray/the-book-of-secret-knowledge#black_small_square-log-analyzers https://github.com/allinurl/goaccess psutil (get system info like CPU, mem, users) Honeycomb https://www.honeycomb.io/blog/tell-me-more-nginx/ Prometheus https://monzo.com/blog/2018/07/27/how-we-monitor-monzo/ Rollbar https://pythonbytes.fm/episodes/show/24/i-have-a-local-pypi-server-and-so-do-you Sentry https://hynek.me/talks/beyond-grep/ others (Datadog, New Relic, Prometheus https://sourcehut.org/blog/2020-07-03-how-we-monitor-our-services/)
* _sink_: log growth roughly linear https://www.youtube.com/watch?v=-6Hk9rcgM94 https://stripe.com/gb/blog/canonical-log-lines

## monitoring

🗄 `python.md` profiling

https://jvns.ca/blog/2022/07/09/monitoring-small-web-services/

healthcheck / heartbeat
* baseline
* db connection https://www.youtube.com/watch?v=GT9WmExDbXQ
* downstream services
* aaS: UptimeRobot, Checkly, lcurl https://www.youtube.com/watch?v=um24VlkkqGo
> I setup a 3rd party service to monitor the heartbeats and the return code to validate they are up and properly returning what I expect, notify me if not. I don't have to do sophisticated response processing at the 3rd party service because I can just use http return codes 99% of the time. The detailed response checking is done at the heartbeat level, then a response code generated. https://news.ycombinator.com/item?id=22823230

---

* users online https://analytics.usa.gov/
* uptime https://news.ycombinator.com/item?id=25553445 depends on system component https://www.openmymind.net/Im-Not-Sold-On-High-Availability/
* _dead man's switch_: cease operation in absence of human operator e.g. carts at airport [Conery 6; think his usage wrong]

* Prometheus https://prometheus.io/docs/introduction/overview/ https://github.com/yolossn/Prometheus-Basics https://softwareengineeringdaily.com/2020/07/09/chronosphere-scalable-metrics-database-with-rob-skillington/

🗄 `link.md` speed
> rf `link.md` then this section

ebpf
* https://news.ycombinator.com/item?id=27435081
* https://www.brendangregg.com/blog/2022-04-15/netflix-farewell-1.html
* https://ebpf.io/what-is-ebpf/

https://www.semicolonandsons.com/episode/error-tracking-and-monitoring
* exception reporting
* logging (production, retention, search)
* downtime alerting
* system monitoring
* financial reporting

* https://hodovi.ch/blog/monitoring-django-applications
* _path_: heuristic for thinking about what to optimize i.e. 99% of your app's execution branches can probably be pretty slow https://blog.phusion.nl/2018/09/18/migrating-passenger-from-cxx-to-go/

load parameters
* _load parameter_: metric; way to describe load on system [Kleppmann 11]
* _node_: CPU, mem, storage 
* _service_: req volume (RPS https://stackexchange.com/performance), simultaneously active users, error rate (5xx per M req), uptime (five nines https://sourcehut.org/blog/2020-06-10-how-graphql-will-shape-the-alpha/)
* _db_: queries per req (statsd) https://www.youtube.com/watch?v=-6Hk9rcgM94 ratio of reads to write, hit rate on cache [Kleppmann 11]

---

* _percentiles_: p50 (median) p90 (worst case); mean doesn't tell you how many nodes/users
* _skew_: uneven distibution re: load across worker processes [Kleppmann 20] what prevents run time of batch job being data divided by throughput

https://news.ycombinator.com/item?id=24006697

* _statsd_: https://github.com/jsocol/pystatsd https://www.youtube.com/watch?v=-6Hk9rcgM94 https://www.datadoghq.com/blog/statsd/ https://docs.datadoghq.com/developers/dogstatsd/ https://www.digitalocean.com/community/tutorials/an-introduction-to-tracking-statistics-with-graphite-statsd-and-collectd https://www.youtube.com/watch?v=R4kMwckrUlg Graphite visualization tool for statsd https://www.digitalocean.com/community/tutorials/how-to-configure-statsd-to-collect-arbitrary-stats-for-graphite-on-ubuntu-14-04

how to start
* _get metrics_: point Uptime Robot at a URL https://www.youtube.com/watch?v=o9ekAeoBXDs https://statusgator.com/ Lighthouse https://forgeperf.org/ https://www.thoughtworks.com/radar/tools?blipid=1158
* _measure metrics_: https://news.ycombinator.com/item?id=23360794
* _sink_: https://serversforhackers.com/s/process-monitoring https://blog.appoptics.com/the-four-golden-signals-for-monitoring-distributed-systems/ https://infrequently.org/2018/09/the-developer-experience-bait-and-switch/ https://3perf.com/talks/web-perf-101/ https://medium.baqend.com/web-performance-made-simple-fc61d81d0c0e http://mediatemple.net/blog/tips/low-hanging-fruit-web-performance/ https://medium.com/observability/want-to-debug-latency-7aa48ecbe8f7 https://ferdychristant.com/amp-the-missing-controversy-3b424031047 https://medium.freecodecamp.org/a-beginners-guide-to-website-optimization-2185edca0b72 https://panic.com/blog/mystery-of-the-slow-downloads/ https://github.com/monitoror/monitoror

black box
* _black box_: user-facing; symptom-oriented
* _options_: https://news.ycombinator.com/item?id=23880071

white box
* _white box_: internals; cause-oriented

## tracing

🗄 `linux.md` tracing

UM
* previous https://developers.signalfx.com/basics/apm.html
> Datadog under hood uses monkey patches whereas signalfx required manual monkey patch
> how does Datadog work under the hood?
* __span__: unit of tracing https://www.elastic.co/guide/en/apm/get-started/current/transaction-spans.html https://docs.splunk.com/observability/apm/span-formats.html
* start/end time, span ID
* can contain / be contained by other spans
* use trace IDs
* tracing system can send span information across network between systems, so you can track a thread of execution across multiple systems
* https://www.youtube.com/watch?v=idDu_jXqf4E https://www.youtube.com/watch?v=YGWA54nEEy0 https://www.youtube.com/watch?v=r8UvWSX3KA8

za
* https://github.com/itamarst/eliot
* https://www.brandur.org/request-ids
* https://microservices.io/patterns/observability/distributed-tracing.html
* https://softwareengineering.stackexchange.com/questions/158198/http-response-header-for-a-unique-request-id-for-rest-service
* https://www.roguelynn.com/words/tracing-fast-and-slow/
* https://danluu.com/perf-tracing/
* https://github.com/JonasKs/django-guid
* https://danluu.com/tracing-analytics/
* https://netflixtechblog.com/building-netflixs-distributed-tracing-infrastructure-bb856c319304

# ZA

* migrate https://news.ycombinator.com/item?id=30942698
* _block-level storage_: hard drive aaS e.g. AWS EBS for db backups
* egress, Cloudfare https://news.ycombinator.com/item?id=28707317
* repl.it https://blog.replit.com/replit-web
* buy don't build https://news.ycombinator.com/item?id=25399250
* dev portal https://github.com/spotify/backstage
* linode vs. digital ocean https://news.ycombinator.com/item?id=26262465 https://news.ycombinator.com/item?id=30352772
* if it's not your data center you're not really self-hosting https://news.ycombinator.com/item?id=27674726 https://github.com/khuedoan/homelab
> But the thing is in most of the companies you don't have full control over the whole stack. Even if you have "full control" over the database, you don't have control over networking, firewall, OS, "security" patching, VMs, Docker, Kubernetes, Load balancers, vendors managing parts of the infra, internet provider, hosting provider ... Not even datacenter team may have control over all of it, but at least that's their job and their area of expertise.

## Cloud Foundry

misc
* _architecture_: DEA (Ruby) Diego (Go) https://docs.cloudfoundry.org/concepts/diego/dea-vs-diego.html
* _healthchecks_: https://stackoverflow.com/questions/39736774/health-check-in-cloud-foundry https://docs.cloudfoundry.org/devguide/deploy-apps/healthchecks.html
* _history_: 2009 (acquired by SpringSource, itself acquired by VMware in 2009) 2011 (public launch)
* `runtime.txt`: specify runtime for Python https://docs.cloudfoundry.org/buildpacks/python/index.html
* _task_: akin to cronjob https://docs.cloudfoundry.org/devguide/using-tasks.html

Pivotal
* _Cloud Foundry_: the software
* _Pivotal Cloud Foundry_: enterprise version
* _Pivotal Web Services_: hosted environment for PCF
* _Cloud Foundry Foundation_: drive adoption to prevent AWS from taking over 😀
* _droplet_: app + dependencies

terms
* _Apps Manager_: GUI
* _pool_: 类似 AWS region ➡️ `AP`
* _lane_: 类似 AWS availability zone ➡️ `AP-3b`
* _org_: account ➡️ `AP-3b FooTeam`
* _space_: namespace within pool/lane owned by org ➡️ `AP-3b FooTeam DEV`

services
* _binding_: service credentials [delivered automatically to app](https://docs.cloudfoundry.org/devguide/services/#application-binding)
* if service listed in `manifest.yml` and service does not exist in CF, app will push but won't start
* _VCAP SERVICES_: JSON of connected services https://banck.net/2014/12/deploying-a-django-application-to-cloud-foundry/

cmds
* login: `login -a <url>`
* switch endpoints: `api <url>`
* view apps in pool: `apps`
* env var for app: `env <app>`
* tail logs: `logs <app>`
* dump logs: `logs <app> --recent`

db setup
* create dedicated db svc
* create db cluster
* create db _in_ cluster
* bind svc to db
* `cf push` app that will need the db

instances
* [kill specific instance](https://stackoverflow.com/a/39241780/6813490)
* [get instance GUID](https://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html#CF-INSTANCE-GUID)
* [route request to specific instance](https://docs.cloudfoundry.org/devguide/deploy-apps/routes-domains.html#surgical-routing)
* [start instances in order](https://stackoverflow.com/a/49417497/6813490)

__app boot__

start command https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html
* https://docs.cloudfoundry.org/buildpacks/prod-server.html
* the console will show you the complete start command on the 'settings' page
* args provided by CLI trump `maninfest.yml`

semantics
* _buildpack_: 
* _droplet_: 
* _Procfile_: Ruby version of `docker-compose.yml`
* used by Heroku

request flow
> if service listed in `manifest.yml` but nonexistant in CF, app won't start
* app binds to route
* create buildpack (`.profile.d`) https://news.ycombinator.com/item?id=28468660
* create droplet
* hooks (`.profile`)
* start (`Procfile`)

__routes__

create route
* _automatic_: CF creates route based on app name/pool and maps route to application on `cf push`
* _custom_: use `manifest.yml` or CLI (`create-route`, `map-route`)
* `manifest.yml` can create routes, but it will not remove previously mapped routes
* can create random route using `cf push <app> --random-route`
* `map-route` runs `create-route` as first step of its own execution so in practice you really only need to use `map-route`; same thing for `delete-route` and `unmap-route`

* commands
```sh
# associate route w/ *space*
create-route <space> <domain> --hostname

# associate route w/ *app*
map-route <app> <domain> --hostname

# rm route and its associations
delete-route <domain> --hostname
```

gotchas
* Gorouter does not use a route until route is _mapped_ to an app; if route created but unmapped, [Gorouter serves 404](https://docs.cloudfoundry.org/devguide/deploy-apps/routes-domains.html)
* you probably have more routes than are visible from Apps Manager; view using `cf routes`
* if you don't explicitly create a route and map it to your application, CF will make the route combining `app-name` and `domain` and `pool-info`
* routes must be unique, even across spaces
> The URL for your app must be unique from other apps hosted by Cloud Foundry - https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html
> Routes are globally unique. Developers in one space cannot create a route with the same URL as developers in another space, regardless of which orgs control these spaces. - https://docs.cloudfoundry.org/devguide/deploy-apps/routes-domains.html#routes

request flow
* client ➡️ Gorouter ➡️ route service ➡️ app
* _Gorouter_: routes w/in pool to app instances via round-robin
* _route service_: handles rate limiting, caching; find app instance using `X-CF-Forwarded-Url` header

## Heroku 

* alternatives https://testdriven.io/blog/heroku-alternatives/

> With something like Heroku, you can have multiple VM's in staging and production, w/ a deployment pipeline that supports rollbacks, monitoring, alerting, autoscaling, all in a managed environment w/ a managed, highly available Postgres setup, with very little effort and 0 maintenance. This is what I've setup at my current startup. My last company was on K8's and I loved it -- but this is nearly as good and requires literally no maintenance and far less expertise / setup. - https://news.ycombinator.com/item?id=22493873 

relisten from 29:30 for limitations https://softwareengineeringdaily.com/2019/06/17/render-high-level-cloud-with-anurag-goel/
> my playbook: Heroku for experiments, Render for most work, AWS for work

cmd
* login: `login`
* create app: `create`
* push: `git push heroku master` [Vincent 📍]
* start: `ps:scale web=1` [Vincent 📍]
* open: `open`
* stop: `ps:scale web=0` https://stackoverflow.com/a/10231477/6813490

* https://www.accordbox.com/blog/deploy-django-project-heroku-using-docker/
* _pricing_: 2GB RAM is hundreds of dollars; they're owned by Salesforce now https://softwareengineeringdaily.com/2019/06/17/render-high-level-cloud-with-anurag-goel/ 29:15
* _dyno_: VM running on top of EC2 instance https://stackoverflow.com/questions/21462439/what-exactly-is-a-single-heroku-web-dyno
* _Git_: seems like when you're logged Heroku automatically becomes a Git remote [Vincent page 📍]
* _scale_: serves 2M req/month pretty easily https://runninginproduction.com/podcast/4-real-python-is-one-of-the-largest-python-learning-platforms-around
* _virtual environments_: doesn't support Poetry yet https://github.com/heroku/heroku-buildpack-python/issues/796 need `requirements.txt` in root https://devcenter.heroku.com/articles/python-support#recognizing-a-python-app https://devcenter.heroku.com/articles/python-support#build-behavior
* _Python version_: `runtime.txt` https://devcenter.heroku.com/articles/python-runtimes#selecting-a-runtime

* analogous to `docker-compose.yml` https://www.mattlayman.com/blog/2019/web-development-environments/
```Procfile
web: ./manage.py runserver
worker: celery worker --app new_hot_thing:celeryapp --loglevel info
frontend: webpack --watch
```

## hosting

* Cloudflare https://rutar.org/writing/how-to-build-a-personal-webpage-from-scratch/ https://rutar.org/writing/previewing-a-development-branch-on-cloudflare-pages/
* https://adamj.eu/colophon/
* s3-website https://bedford.io/misc/about/
* https://brianli.com/about/
* Netlify https://uglyduck.ca/articles/
* node (physical or virtual) to host something (web server, API)
* _physical_: DIY (Raspberry Pi) real deal (Rackspace costs $100s/month) https://news.ycombinator.com/item?id=22407098
* _virtual_: easy clouds (Netlify, Github) complex clouds (AWS et al.) domain name company (NameCheap, et al. will do this for you)
* BYO https://news.ycombinator.com/item?id=30676595

static site
* Netlify https://wsvincent.com/site-design/ https://adamwathan.me/uses/
* Github: source has to be public
* AWS: https://brandur.org/aws-intrinsic-static S3 and Cloudfront https://www.benkuhn.net/about/
* Firebase https://tinyprojects.dev/projects/tiny_website

## GCP

* _RTDN_: notifcations from GP app https://developer.android.com/google/play/billing/rtdn-reference
* howto https://developer.android.com/google/play/billing/getting-ready#enable-rtdn
* _Cloud Pub/Sub_: MQ btw GCP apps https://cloud.google.com/pubsub/docs/publish-receive-messages-console https://console.cloud.google.com/cloudpubsub/topic/list https://console.cloud.google.com/cloudpubsub/subscription/list
* multiple topics for GP app: possible? https://stackoverflow.com/q/72688883 yes https://stackoverflow.com/a/52759477 https://stackoverflow.com/a/71740580 no https://stackoverflow.com/a/70986770
* https://stackoverflow.com/questions/6991135/what-does-it-mean-to-hydrate-an-object

IAM
* _principal_: user account, service account, group
* _role_: collection of perms
* _condition_: further constraint on role i.e. no write access if req lacks key
* _allow policy_: mapping of principal to role per resource https://cloud.google.com/iam/docs/policies
* _service account_: account for service (vs. user) https://cloud.google.com/iam/docs/service-accounts
* GCP also has service accounts for itself e.g. to publish RTDN https://stackoverflow.com/a/64184564

IAP Proxy https://www.youtube.com/watch?v=xM9-FSU5MoY
* type of access: public, authed users, authed employees [2:00]
* = identity service in front of site [3:30]
* uses Google (or Active Directory) as SSoT for identity [4:15]

za
* unreliable https://news.ycombinator.com/item?id=24169044
* bad customer supprt https://calpaterson.com/amazon-premium.html
* GCS = S3
* Cloud SQL = RDS
* Cloud Spanner = Aurora
* _BiqQuery_: serverless db
* _BigTable_: BigQuery but NoSQL https://cloud.google.com/free/docs/map-aws-google-cloud-platform
