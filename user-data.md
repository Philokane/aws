#!/bin/bash
yum update -y
yum install httpd -y
service httpd start
chkconfig httpd on
cd /var/www/html
echo "<b>Your Internal IP Address is:</b> " >> index.html
curl http://169.254.169.254/latest/meta-data/local-ipv4 >> index.html
echo "<br><b> Your External IP Address is: </b>"$'\r' >> index.html
curl http://169.254.169.254/latest/meta-data/public-ipv4 >> index.html
echo "<br><b> Your DNS Address is: </b>"$'\r' >> index.html
curl http://169.254.169.254/latest/meta-data/public-hostname >> index.html
EC2_INSTANCE_ID=$(curl -s http://169.254.169.254/latest/meta-data/instance-id)
EC2_AVAIL_ZONE=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)
EC2_REGION="`echo \"$EC2_AVAIL_ZONE\" | sed -e 's:\([0-9][0-9]*\)[a-z]*\$:\\1:'`"
Hostame: $(hostname -f) na
