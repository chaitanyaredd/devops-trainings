# Auto-scaling-group
- Auto scaling groups are collection of EC2 instance that will automatically adjust capacity based on the decmand.
- Along with auto scale-in/scale-out features auto scaling group provide ** fleet mangement features **
    - Replacing the failed instances,
    - load balancing,
    - ensuring right number of server are running inorder to keep application healthy.

# Usecase: Deploy nginx applicaiton using autoscaling group & scale-out EC2 instances from desired capacity 2 to max capacity: 5

- Create Launch template [nginx-webserver]
    - name: nginx-webserver
    - Version: 1.0
    - AMI: Amazon-Linux
    - instance type: t2.micro
    - Keypair
    - securitygroups

- Create Target group without registering node
    - name: bdx-tg
    - VPC
    - protocol: http
      port: 80
    - Applicaiton running default path so we can healthcheck '/' as default
    - Don't register nodes

- Create applicaiton load balancer
    - name: bdx-alb
    - vpc & subnets to which alb can route traffic.
    - Give protocol[http] & port[80] that the listener will check for incoming traffic
    - Forward the traffic to respective target group [bdx-tg] from default listener.

-  Create auto scaling group
    - name: bdx-asg
    - Tempalte: nginx-webserver
    - vpc & subnets where to launch instances
    - Integrate with ALB & its target group
    - Provide desired[2], min[2] & max[5] capacity
    - Update dynamic scaling policies, by adding the cpu usage more than  50% scale-out the instance.
    - Create

- Now applicaiton is accessible from applicaiton load balancer dns name.    

- Now test the scale-out & scale-in features
  Keep stress on all cpus of ec2 - Run this comamnd on all ec2's
  stress --cpu $(nproc) --timeout 300 

- After few minitutes new machine created & we can check this activity in the ASG activity log.

