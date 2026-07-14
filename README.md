# Terraform_security_group
 ```.tf
root@ip-172-31-38-5:~# cat resource.tf 
resource "aws_eip" "eip" {
  domain   = "vpc"
  instance = aws_instance.ec2.id
}

resource "aws_instance" "ec2" {
  ami                    = var.ami
  instance_type          = var.ec2_type
  key_name               = var.key
  vpc_security_group_ids = [aws_security_group.sg.id]


  root_block_device {
    delete_on_termination = true
    volume_size           = 10
    volume_type           = "gp2"
  }

  tags = {
    Name = "serve-2"
  }
}

resource "aws_security_group" "sg" {
  name        = "test-sg"
  description = "this is the test sg for terraform"
  vpc_id      = "vpc-0a4b65dd0bbcc4ed9"


  tags = {
    Name = "<S-F1>test-sg-tag"
  }
}

resource "aws_vpc_security_group_ingress_rule" "inbound" {
  security_group_id = aws_security_group.sg.id

  cidr_ipv4   = "0.0.0.0/0"
  from_port   = 22
  ip_protocol = "tcp"
  to_port     = 22
}

resource "aws_vpc_security_group_egress_rule" "out" {
  security_group_id = aws_security_group.sg.id
  cidr_ipv4         = "0.0.0.0/0"
  ip_protocol       = "-1" # semantically equivalent to all ports
}
```

```
vim var.tf
root@ip-172-31-38-5:~# cat var.tf 
variable "ami" {
  default = "ami-01a00762f46d584a1"
}

variable "ec2_type" {
  default = "t3.micro"
}

variable "key" {
  default = "ved1"
}
```
