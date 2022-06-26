# Course Overview
1.AWS Cloud Concepts
2.AWS Core Services
3.AWS Security
4.AWS Architecting
5.AWS Pricing and Supporting


Core services

	Amazon Elastic Compute Cloud 
		SSH - Private Key
		HTTP

	Amazon Elastic Block Store
		HDD / SSD
		same availibility zone with EC2
		Tag for EBS
		encryption in EC2
		attach volumn into Linux (lsblk mke2fs mount)

	Amazon Simple Storage Service S3
		Create bucket to store data
		Key(file path)->Object->bucket
		Data redundantly Stored in same region
		Path should be globally unique

	AWS Global Infastructure
		Global inrastrcucture, breakdown to 3 topics:
			region (geographics zone, map)
				resource in one region are NOT replicated to other regions automatically

			availibility zone
				data center in a region
				connect with each other in high speed network
				handle data redundancy & availablity for one region

			edge location
				CDN, amazon cloud front
				routine request to the closet availability zone & region
		
	Amazon Virtual Privae Cloud
		create private & virtaul network inside AWS cloud
		network control (IP, subnet, route tables)
		control incoming outcome traffic
		EC2 components to VPC
		VPC within a region across AZ
		IPs -> Subnets
		Subnet, could be public (expose to Internel) / private
		Subnet can talk with each other by default
		Internet Gateway (IGW), for subnets exposed to Internet


	AWS Security Group
		work as firewall
		multi tiers security group
		one tier only accepts traffic from particular tier


	Application Load Balancer
		second level elatic load balancer
		Features:
			path and host-based routing (domain request)
			native IPv6 support virus VPC
			deletion protection & request tracing 
			AWS WAF (firewall integration)
			dynamic ports
		Listener & Target & Target Group
		Load Balancer -> Listener -> Target Group -> Target

	Auto Scale
		Add / remove EC2 instance
		Amazon Cloud watch alert
		Components:
			Launch Configuration
			Auto Scaling Group
			Auto Scaling Policy

	Amazon Route 53 (DNS)
		Internet provider->Amazon Route 53 (DNS)
		hostzone = IP record set
		internal / external
		shorten DNS resolution of customers


	Amazon Relational Database Service (RDS)
		Instance = Class + Storage + DB Engine
		Read replica instance


	Amazon Lamda
		let you run code without provisioning & managing service
		only pay computing you use (not full time running as server)
		event driven computing?
		suppose to support serverless & micro-service applications
		user case
			auto backup
			process object & upload S3
			event driven log analysis
			event driven transformation


	Amazon Elastic Beanstalk
		run service on cloud
		PaaS
		quick deployment, across language
		application->environment (webserver vs. worker longtime)


	Amazon Simple Notification Service (SNS)
		Pub/Sub messaging to Lamda & SQS (MQ?)
		send message to mobile
		decouple & scale micro-service
		policy->subscription


	Amazaon Cloud Watch
		monitor resource & application on real time
		resource / application status watch->alarm->notification/scale
		metric
		cloud alarm-> watch single metric->trigger one or more actions

	Amazon Cloud Front
		Content delivery network / CDN
		cache to edge location


	AWS Cloud Formation
		Manage service / resource
		Tempalte file -> provision resource -> stacks
		same template to create differnet env, parameter depends
		infrastructure as code
		Template->Permission->Cloud Formation


AWS Architecute
	AWS Architecure 5 Pillars:
		security
			identity and access management IAM
			Detective controls
			infrastructure protection
			data protection
			incident response
			Design Principle:
				Implement security at all layers
				Enable traceability
				Apply principle of least rriviledge
				Focus on securing your system
				Automate
		reliability
			Recover from issues/failures
			Apply best practice in
				Foundations
				Change Management
				Failure management
			Anticipate, respond and revent failures
			Design Principles:
				Test recovery procedures
				Automatically recover
				Scale horizontally
				Stop guessing capacity
				Manage change in automation
		performance efficiency
			Select customizable solutions
			Review to continually innovate
			Monitor AWS services
			Consider the trade-offs
			Design Principle:
				Democratize advanced technologies
				Go global in minutes
				Use a serverless architectures
				Experiment more often
				Have mechanical sympathy
		cost optimization
			use cost-effective resources
			Matching supply with demand
			Increase expenditure awareness
			Optimize overtime
			Design Principle:
				Adopt a consumption model
				Measure overall efficiency
				Reduce spending on data center operations
				Analyze and attribute expenditure
				Use managed services
		operational excellence
			Manage and automate changes
			Respond to events
			Define the standards
			Design Principle:
	Fault Tolerence & High Availability System
		Fault Toerance
			Ability of a system to remain operational
			Built-in redundancy of an application's components
		High Availability
			Systems are generally functioning and accessible
			Downtime is minimized
			Minimal human intervention is required
			Minimal up-front financial investment
		High Availability Service Tools
			Elastic Load balance
			Elastic IP address
			Amazon Route 53
			Auto Scaling
			Amazon CloudWatch
		Fault Tolerance Tools
			Amazon Simple Queue Service
			Amazon Simple Storage Service
			Amazom Relational Database Service
	Web Hosting
			
AWS Seurity
	


