**Date: 2nd Septenber, 2026**

#IAM ROLES
------------
IAM roles are much like users in the sense that they are identities you can create and
add a permission to it to determine what they can and can not do. However, instead of
them being tied to one person or user accound, an IAM role is assumable by any
individual or account that needs it. A role also does not have credentials associated
with it, iinstead whrrn you assume the role, you are provided with secret temporary
credentials for just that session. You can use it to deligate access to users, services
and applications that normally do not have access to your aws services.
[Account access manager](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)
 is an iam feature that lets you centrally assign iam roles 
across your organisation's account to iam iidentity center users and groups. IAM 
identity center is a service that alllows you to manage user access and sigh-in 
credentials accross multiple aws accounts and application from onr central place. 
Before deleting a service-linked role, you must first delete their related resource.
A sercice role is an iam role that a service assumes to perform actions on your behalf.
a service-linked role is a type of service role that is linked to an aws service. The 
service can assume the role to perform an action on your behalf. these roles are owned 
by thhe service. An iam administrator can view but not edit the permissions for service
lined roles. Role chaining is the proccess of assuming a role from another role.
Delegation is the granting of permission to someone to allow access to resources you 
control. To delegate a role to someone, you create an iam role in the trusting account
or the account allowing the assuming of the role that has two policies, the permission 
policy which grants permission to the user of the role to carry out intended tasks. 
The trust policy which soecifies which trusted account members are allowed to assume 
the role. Trust policy is a json document in which you define the principals that you
trust to assume the role. The principals you can specify in the trust policy includes 
users, roles, accounts and services. 

##Using an IAM role to grant permissions to applicatiions running on Amazon EC2 
instances
--------------------------------------------------------------------------------
Instead of having to manually add access keys to instances whenever they need to access
other aws services, you can just create a role that the instance can assume. An 
application running on an ec2 instance is abstrated from aws by the virtualized 
operating system be cause of this, you need to create an instance profile in order to 
be able to assign a role to the ec2 instance. The instance profiile contains the role 
and can provide the temporary credentials of the role to an application that runs in
the instance. The temporary credentials can then be used in the application's api calls
to access resources and to limit access to only those resources that the role specify.
Only one role can be assigned to an instance at a time and all applications in the 
instance share the role and permissions. 

Roles beat access keys iin my opinion because you do not have to share or manage 
credentials and the credentials for roles are temporary and reset after every session
so it is safer and more secure.


**BUILD**
I created an s3 bucket and uploaded a file into it, i also created an iam role and 
named it ec2-s3-read-role. i then lauched an ec2 instance and added the created role 
instance profile. i was able to list the files and folder in my bucket and list the 
buckets itself but could not copy a file into the bucket.

**check**
the credentials arrive through the instance metadata service(IMDS), reachable inside 
the instance so the instance obtains the credentials from there authomatically and 
assumes the role.
the two policies attached to the role is the trust policy which determines what service
or user can assume the role and the permission policy which specifies what the user who
assumes the role can and can not do in my account.


so i covered creating an instance, an s3 bucket, a role with trust policy and 
permission and the ec2 instance assuming the role to access my s3 bucket.


