# Terraform-LB root@ip-172-31-41-79:~# cat resource.tf
```.tf 
resource "aws_instance" "ec2" {
  ami                         = var.ami
  instance_type               = var.instance_type
  key_name                    = var.key_name
  associate_public_ip_address = true
  vpc_security_group_ids      = var.sg
  user_data                   = <<EOF
#!/bin/bash 
sudo -i 
apt update 
apt install nginx -y 
systemctl start nginx 
systemctl enable nginx 
echo "this is server created from terraform " > /var/www/html/index.html 
EOF 
  tags = {
    Name = "server-2"
  }
}

variable "ami" {
  default = "ami-01a00762f46d584a1"
}
variable "instance_type" {
  default = "t3.micro"
}

variable "key_name" {
  default = "ved1"
}

variable "sg" {
  default = ["sg-0c52d84df5dfd1dc4"]
}

variable "subid" {
  default = ["subnet-0c3f510ad5802faf0", "subnet-0b34028d74921abc3", "subnet-0aee1a6604f19a3f4"]
}


resource "aws_lb_target_group" "tg1" {
  name     = "test-tg"
  port     = 80
  protocol = "HTTP"
  vpc_id   = data.aws_vpc.default.id
  health_check {
    path                = "/"
    protocol            = "HTTP"
    matcher             = "200-399" # FIXED
    interval            = 30
    timeout             = 5
    healthy_threshold   = 2
    unhealthy_threshold = 2
  }
}


resource "aws_lb_target_group_attachment" "lb-tg" {
  target_group_arn = aws_lb_target_group.tg1.arn
  target_id        = aws_instance.ec2.id
  port             = 80
}



resource "aws_lb_listener" "alb-ls" {
  load_balancer_arn = aws_lb.lb.arn
  port              = 80
  protocol          = "HTTP"

  default_action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.tg1.arn
  }
}


resource "aws_lb" "lb" {
  name               = "alb-lb"
  internal           = false
  load_balancer_type = "application"
  subnets            = var.subid
  security_groups    = var.sg

  enable_deletion_protection = false

  tags = {
    Name = "app-lb"

  }
}

## output block 
output "lb_dns_name" {
  value = aws_lb.lb.dns_name
}
```
# Data block root@ip-172-31-41-79:~# cat data.tf 
```.tf
data "aws_vpc" "default" {
  default = true
}

output "vpc" {
  value = data.aws_vpc.default.id
}
```


# Launch Template root@ip-172-31-35-224:~# cat auto.tf 
```.tf
resource "aws_launch_template" "example" {
  name_prefix   = "example-template"
  image_id      = var.ami # Use valid Ubuntu AMI
  instance_type = "t2.micro"

  vpc_security_group_ids = var.sg

  user_data = base64encode(<<EOF
#!/bin/bash
sudo apt update -y
sudo apt install nginx -y
systemctl start nginx
systemctl enable nginx
sudo echo " this si test server" > /var/www/html/index.html
EOF
  )
}

# Auto Scaling Group
resource "aws_autoscaling_group" "example" {
  name                = "example-asg"
  min_size            = 1
  max_size            = 3
  desired_capacity    = 2
  vpc_zone_identifier = ["subnet-0c3f510ad5802faf0", "subnet-0b34028d74921abc3"]

  launch_template {
    id      = aws_launch_template.example.id
    version = "$Latest"
  }

  health_check_type         = "EC2"
  health_check_grace_period = 300

  tag {
    key                 = "Name"
    value               = "nginx-server"
    propagate_at_launch = true
  }
}
```
