# AWS VPC PEERING PROJECT

This project aims at understanding AWS peering connnection between two VPC's in a particular region name "us-east2"

**Pre-requisite**

- AWS Account
- IAM permission to create and delete resources

**Steps**

1. Firstly create a VPC using the console in the "us-east2" region.

2. Providing name as "test-vpc" & selecting CIDR as "10.0.0.0/16". CIDR is important because resources needs to get an IP address in a certain range.

3. Keeping tenancy as "Default" as we dont want to get unecessary cost by keeping as "Dedicated" .

4. Click on "Create VPC" to create one.

5. Next creating Subnet by naming as "my-test-public-subnet" for Public VPC and selecting our VPC from the dropdown.

6. We will give IPv4 subnet CIDR as "10.0.0.0/24" so out of 65k IP's , 256 IP's are allocated to this Public Subnet.

7. Then we will create the Subnet by clicking on "Create Subnet".

8. Next we will create the resource inside this public subnet which will be an EC2 resource.

9. Create an Ubuntu Ec2 instance by selecting our VPC and subnet in Network settings.

   10.Next creating internet gateway and route table to make it publically accessable.

10. Same way we will follow for "Prod VPC" by creating yet another VPC. ANd giving IP address as "192.0.0.0/16" .

11. After creating all the resources such as inernet gateway, subnet, route table , we created EC2 for Prod Server. In prod EC2 we also allowed custom http connection and allowed CIDR of our private VPC

12. Our main aim is to ping the server in the test environment from prod server.

13. Then we tried to ping from our test ec2 server to our prod . It didnt happen. For this we then established VPC peering connection from Test to Prod.

14. But still after pinging it didnt happen. Then we found out we have to configure route table in such a way so that it will allow the communication in between servers from different VPC.

15. Then we go to the Test route table and edit routes by putting the CIDR of the Prod VPC and selecting the peering connection in target.

16. Doing the same thing for Prod Route table by putting the VPC CIDR of Test and giving the target as peering connection.

17. Then the last process will be to allow ICMP in the security groups of both the test and prod Server.

18. After doing this, when we try to ping the servers from test-prod / prod-test , there is no data loss & the packets are transferring.
