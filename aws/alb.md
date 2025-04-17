# Network Load Balancer
- NLB works on L4 (Transport layer) of OSI model.
- It handles on TCP/UDP traffic.
- NLB mainly used in applicaitons where high throghput required & low latency based app's

# Application Load Balancer
- ALB works on L7(application layer) of OSI model
- It handles http & https traffic along with TCP/UDP traffic.
- ALB mainly used applications header based, path based routing required applicaions.

# Create applicaiton load balancer
- Choose the name: bdx-alb
- Scheme:
    ** Internet facing: **
    - The client over the internet can access the DNS of this loadbalancer. 
    - Also the nodes that are associated with this load balancer are present inside the public subenet.
    - So when we do DNS lookups its resolved the PUBLIC IP of target.
    ** Internal facing: **
    - The clients who are having access to the VPC they can access the this DNS of this loadbalancer.
    - The nodes associated with this loadbalancer are present in private subnet.
    - When we try to do DNS lookup its will try resolve to the private IP of target.
- Choose the VPC & subnet that loadbalancer would like to send traffic.
- ** Define Listener & routing**
    - Listener is process that checks the incoming requests to load balancer based on specific protocol & port later routes the request to target groups based on default action & additional rules that we have defined inside the listener.
    - Allow incoming traffic for the port that we expect traffic.

# Target group
- Target group contains set of targets that can handle the traffic that listener forwarded from ALB.
- Also the ALB will verify the health of the target once the target group associated with ALB.

# Create target group
- Choose targets type as Instances
- set name for targetgroup: bdx-tg
- provide the protocol & port on which applicaitons running
- Provide healthcheck path for applicaiton based on that ALB will decide whether node is healthy or not.
- Provide VPC details from which targets will be choosed. 

# Achieve path based routing in applicaiton load balancer
- Create VPC & four public subnets
- Create 4 EC2 machines in 4 different subnets
- Install nginx in first two webservers
  yum install nginx -y
  echo "This is webserver-1"
  systemctl start nginx
- Install nginx in other two webservers & create customer folder under /usr/share/nginx/html/images/index.html
- Create target group[tg-1] for nginx webservers
- Create target group[tg-2] for custom nginx webservers & health check should be /images/
- Create application load balancer & create listeners(default rule point protocol:http & port:80 of loadbalncer traffic to the target-group[tg-1])
- Create one more rule in the listener to point custom based rule to targetgroup [tg-2]

# PENDING - ITEMS
- TARGETGROUP STICKENESS
- PRIORITY IN RULES
