Security Groups in AWS are virtual firewalls attached at the EC2 instance level.

They control inbound and outbound traffic.

Security Groups are stateful, meaning if inbound traffic is allowed, the response traffic is automatically allowed back, even without explicitly creating outbound rules for that response.

For example, if I allow SSH inbound on port 22 from my laptop IP, the return traffic from EC2 to my laptop is automatically permitted.

By default, AWS allows all outbound traffic in Security Groups, but in production environments we usually restrict outbound access based on security requirements.

Unlike Security Groups, NACLs are stateless, so both inbound and outbound rules must be explicitly configured.



#### Example 
- Your laptop IP = 1.2.3.4
- EC2 server running web application
- Security Group allows:
- Type	Port	Source
- SSH	22	Your IP
- HTTP	80	0.0.0.0/0

Now when you SSH into EC2:
 - Step 1: Inbound rule allows:
	Your Laptop → EC2 : Port 22

 - Step 2:
	- EC2 sends response back to your laptop.
	- Even if outbound rule is not explicitly configured for that response:
	- EC2 → Your Laptop
	- AWS automatically allows it because Security Groups are stateful.

