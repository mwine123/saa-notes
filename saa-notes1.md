# DOMAIN 1- DESIGN SECURE ARCHITECTURES
 ---------------------------------------
##Shared Responsibility Model
Started by going over the amazon shared responsiblity model. Security in and security 
of the cloud. The shared responsibility model tells what the customer is responsible
for and what the service provider is responsible for.
The customer is responsible for data and the configuration of access controls that
reside in AWS. Cloud service provider is generally responsible for the underlying 
infrastructure.

**Responsiblity in the cloud**
If you can configure or store it then you (the customer) are responsible for it.

**Responsiblity of the cloud**
If you can not configure it then the cloud service provider is responsible for it.

##IAM
IAM is a permission and access management service used for security on aws. It is a web
service that helps you securely control access to aws resources. It is used for 
authentication (who can sign in) and authorization (has permission) to use aws 
resources. A policy is an objject in aws that when associated with an identity or
resource defines their permission. AWS supports nine types of policies. Identity-based
policy, resource based policy, VPC endpoint policy, permission boundaries, AWS 
organisation service control policies(SCPs), AWS organisations resource control policy
(RCPs), Access control lists(ACLs), Resource access management shares(RAM) and sessions
policies. A permission is a statement in a policy that allows or denies something.

**BUILD**
I created a user named test-user-1 and two groups, read-only-testers which had 
AmazonS3ReadOnlyAcess and deny-s3-readonly-group which denied AmazonS3ReadOnlyAccess.
I put the user into the read-only-testers group initially and the user had access to 
view s3 buckets, list what is in the bucket and also download the files in the bucket
but could not create buckets. i then added the user to the deny-s3-readonly-group 
group while the user was still in the read-only-testers group just to see what happens 
and the user was denied access to viewvs3 buckets. An explicit deny always overrides 
and allow.

**Check**
Policies are stored separately and then attached to a user or group when needed.


##Vital Notes
I covered shared responsibility model and IAM. So far, i came across some new cloud
computing models ive never seen and that confused me. There was function as a service.
Funtion as a Service iis when you write a function and it is executed when something 
triggers it. You do not need to provision or manage andy resources, just the code.
