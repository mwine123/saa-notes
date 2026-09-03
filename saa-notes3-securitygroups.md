**2nd September, 2026**

# SECURITY GROUPS
------------------
A security group controls the traffic that is allowed to reach and leave the resources
that it is associated with. Whhen you create a VPC, it comes with a default security 
group but you can create additional security groups for a VPC. You can specify the 
source, port range and protocol for each inbound rule and the destination, port range,
and protocol for each outbound rule. You can assign a security group to multiple 
resources and multipe security groups to one resource. Security groups are stateful,
which means when the rules are checked when traffic is going in, it is remembers so the 
rules arent checked again when teaffic is coming out, responses from traffic that was allowed
into an instance is allowed out regardless of outbound rules.

# NETWORK ACL
--------------
Network acls deny or allow specific inbound or outbound network traffic at the subnet 
level. you can use the default network acl for you vpc or configure custom ones. custom
acls add additional layer of security. each subnet in a vpc must be associated with a 
network acl, if you do not associate it wiith a network acl, the subnet is authomatically
associated with the default acl of the vpc. you can associate multiple subnets with one 
network acl, however you can not associate multiple nacls with one subnet. once you associate
it with a second acl, the previous one is removed. you can only have 32766 rules per network
acl and rules are evaluated from the smallest number when determining whether to allow or
deny traffic. if a traffic matches a rule and the ruls is applied, no additional rules 
are evaluated. It is recommended to create rules incrementally of 10s or 100s so that 
we can add more rules in between latter on if needed. The rules are evaluated when 
traffic enters or leaves the subnet. it is state less whichh means if traffice enters 
the subnet, the infomation isnt saved so when a response is going out of the subnet, unlike
security groups, the network acl evaluates the rules again so depending on the rules, 
the response may or may not be allowed to leave the subnet. network acls can not block
dns requests or requests from the route 53 resolver, it cannot block traffic to instance
metadata service(IMDS). it does not filter traffic destined to and from the dns, dhcp,
instance metadata, task metadata endpoint, lincense activation for windows instances,
amazon time sync service and reserved ip addresses used by the default vpc router.

## BUILD
i configured an ec2 isntance and allowed http access from anywhere in the inbound rules
and ssh from my ip in the inbound rules but i couldnt instance connect so i went back 
to try and fix that by adding another inbound rule for the published ip for instance 
connect aws uses and it didnt work. i think it was a wrong one but for now i changed the
ssh rule to allow ssh from anywhere jjust for this lab but i know it is not a best 
practise. i installed nginx on the instance and viewd the ip in a browser and got the 
wlcome to nginx page then i deleted the iinbound rule that allows http and refreshed the 
browser and it has been loadiing for some time now with no end in sight. i think it is 
hanging. added the http rule back and it works again. my last test was to deny http 
access in the inbound rules of the network acl in the subnet level and the browser 
hung again.

**CHECK**
---
if i allow an inbound on a security group an outbound is not needed because it remembers
the request, no matter what the outbound is, a response will come.(stateful). NACL 
however is different, it checks its rules on every pass, so when traffic is going in, it 
checks the inbound rules and checks the outbound when traffic is coming out. if you do
not allow at the in the outbound rules, the response wont be allowed to leave the subnet.

once again explicit deny overwrites allow. network acls allow and deny traffic at the 
subnet level and security groups allow traffic at the resource level. 
