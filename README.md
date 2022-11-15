# cloudwatch
CloudWatch is a handy feature that helps with event correlation and is critical in maintaining visibility within your technical infrastructure.
Prerequisites: -

1. An AWS account.
2. IAM user with AWS management console access.
3. IAM permission is required to perform IAM, EC2, and CloudWatch activities.

Run the following commands at the console to download and install the Amazon CloudWatch agent on target machine:

1. wget https://s3.amazonaws.com/amazoncloudwatch-agent/debian/amd64/latest/amazon-cloudwatch-agent.deb
2. sudo dpkg -i -E ./amazon-cloudwatch-agent.deb
3. Download and install the collectd daemon:
4. sudo apt-get update && sudo apt-get install collectd
5. Create the Amazon CloudWatch configuration file by running the Amazon CloudWatch configuration wizard:
6. sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard

Create an AWS credentials file with the AWS access key ID and shared access key at /home/.aws/credentials with the following content. Replace the AWS-ACCESS-KEY-ID and AWS-SECRET-ACCESS-KEY placeholders with the keys obtained in the previous step:

1. sudo apt install awscli
2. aws –version
3. aws configure
[default]
  aws_access_key_id=AWS-ACCESS-KEY-ID
  aws_secret_access_key=AWS-SECRET-ACCESS-KEY
  
#Edit the common configuration file for the Amazon CloudWatch agent at /opt/aws/amazon-cloudwatch-agent/etc/common-config.toml and specify the path to the credentials file created in the previous step.

sudo vi /opt/aws/amazon-cloudwatch-agent/etc/common-config.toml

#Update the file with this content:
[credentials]
  shared_credential_file = "/home/bitnami/.aws/credentials"

#Start the Amazon CloudWatch agent with the following command:
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s

#Check that the agent is running with the following command:
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status

#Check that the agent is running with the following command:
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
 
The above steps will also automatically configure the Amazon CloudWatch agent to automatically start on server reboot.
