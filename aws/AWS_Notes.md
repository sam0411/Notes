5-25

IAM
Root -> IAM User, Group, Permission

Role , Temporary

ELB within region balancing
Route53 across regions balancing


EC2
	public key & private key, private key only can download once, public key store in AWS
	login key name & private key

	root volumn, data volumn

	Block store device
		EBS (Elastic Block Store)
			network attached network drive
			persistent
		instance store
			dispear after reboot


VPC
	vpc is region specific
	subnet is az specific
		subnet must associate with a route table

	CIDR IP address range (RFC)
	implied router
	router table
	internet gateway = from inside to access network
	virtual private gateway = for external accessing
	securrity group
	network acces control list -> subnet

	IP Addressing
		once VPC created, can not change CIDR block
		10.0.0.0/24
			total 32 bit, first 24 for network, last 8 for hosts (256 hosts, 0-255)
			range /28 - /16
			no ip overlap among subnets in vpc
			each subnet first 4 + last 1 IP, reserved by AWS
				10.0.0.0 base network
				10.0.0.1 router
				10.0.0.2 dns
				10.0.0.3 reserved for future
				10.0.0.255 last IP

	by default, each region has default VPC, each AZ has 1 subnet

	Internet Gateway
		one IGW per VPC

	ENI (Elastic network interface), security group bulit on it (virtual firewall)

	up to 5 security group to EC2

	stateful: inbound permitted, outbound auto permitted (for same destination)

