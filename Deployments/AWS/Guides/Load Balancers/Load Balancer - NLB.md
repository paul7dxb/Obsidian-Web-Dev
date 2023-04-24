# Network Load Balancer

- Requires EC2 instances with service to be used be load balancer
	- Load balancer used for HTTP or HTTPS traffic
	- Example a web server

- Go to Load balancers in the EC2 section (tab on left pane)
- Create Instance
- Choose type (NLB)

- Choose AZ
	- IP assigned by AWS or use Elastic IP
- Assign [[Target Group]]


# Cleanup

- Delete NLB
- Delete target group
- Delete rules for instances if different