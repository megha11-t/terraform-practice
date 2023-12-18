resource "aws_kwy_pair" "mykey" {
  key_name="terra-key"
  public_key=file("/home/ubuntu/.ssh/terra-key.pub")
}

resource "aws_default_vpc" "default_vpc" {

}

resource "aws_security_group" "allow_ssh" {
  name        = "allow_ssh"
  description = "Allow ssh inbound traffic"

  # using default VPC
  vpc_id      = aws_default_vpc.default_vpc.id
  ingress {
    description = "TLS from VPC"

    # we should allow incoming and outoging
    # TCP packets
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"

    # allow all traffic
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "allow_ssh"
  }
}
resource "aws_instance" "my-vpc-instance" {
 key_name= aws_key_pair.mykey.key_name
ami= var.ec2-ubuntu-ami
 instance_type= "t2.micro"
 security_groups= [aws_security_group.allow_ssh.name]

 tags {
   Name= "Secured-instance"
   }
}

