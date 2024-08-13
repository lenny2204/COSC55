# COSC55 Milestone
Identifies the topic area that you are interested in exploring
- Developing network traffic control policies using various firewalling techniques

The AWS Services that are relevant to that topic
- AWS Security Groups: Control inbound and outbound traffic for EC2 instances.
- AWS Network Access Control Lists: Add a layer of security for VPC subnets; control traffic at subnet level
- AWS Web Application Firewall: Protects web apps and allows creating rules to filter web traffic
- AWS Firewall Manager: SImplifies firewall rules across different AWS accounts
  
At least 3 links to references, tutorials, documentations that you might use to implement the service (this can be a separate page as it might be good to have a References Page on the site going forward)
- https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html
- https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html
- https://docs.aws.amazon.com/waf/latest/developerguide/fms-chapter.html
- https://www.barracuda.com/support/glossary/aws-firewall
- https://www.tufin.com/blog/firewall-policy-planning-crafting-robust-network-defense



PART 2: Diagram/Plan
![image](https://github.com/user-attachments/assets/1e927ec5-a92e-4b14-b341-d3e16ed2648b)
More detailed labels of Diagram:
1. AWS Firewall Manager ("Firewall")
   - Role: Centralized Security Policy Management System
   - Purpose: Manages and enforces firewall rules across all AWS security services, ensuring consistent protection across the cloud environment. 

2. Network Access Control Lists (NACLs):
   - Role: Subnet-Level Traffic Control System
   - Purpose: Adds a layer of security at the subnet level, controlling inbound and outbound traffic by allowing or denying specific IP addresses, protocols, and ports;   
     ensure that unauthorized traffic does not reach internal resources within the VPC.

3. VPC (Virtual Private Cloud):
   - Role: Isolated Network Environment
   - Purpose: Serves as the foundational networking layer in AWS, containing and managing subnets and their associated resources; ensures secure and isolated communication   between resources while helping define IP address ranges, route tables, and internet gateways.

4. Private Subnet:
   - Role: Internal Database Server Hosting
   - Purpose: Hosts critical internal resources such as database servers that should not be directly accessible from the internet; isolates sensitive data and services, limiting access only to internal resources or specific external services via controlled routes.

5. Public Subnet:
   - Role: Public-Facing Web Server Hosting
   - Purpose: Hosts web servers and other resources that need to be accessible from the internet; allows external users to access the web application, while security measures ensure that only legitimate traffic reaches these resources.

6. Security Groups:
   - Role: Instance-Level Access Control Systems
   - Purpose: Attached to individual EC2 instances, Security Groups act as stateful firewalls that control inbound and outbound traffic based on defined rules; ensure that each instance only communicates with approved sources and destinations, protecting against unauthorized access.

7. AWS Web Application Firewall (WAF):
   - Role: Web Application Security Layer
   - Purpose: Positioned in front of the public web server, the WAF protects the web application by filtering incoming HTTP/HTTPS requests. It blocks web exploits like SQL injection and cross-site scripting (XSS), ensuring that malicious traffic does not compromise the application.

8. Inbound/Outbound Traffic:
   - Role: Data Flow Management
   - Purpose: Represents the flow of data entering and leaving the subnets and instances. This traffic is managed and filtered by Security Groups, NACLs, and the WAF to ensure that only authorized traffic reaches my AWS resources, maintaining the integrity and security of the environment.

My Plan:
1. Creation/Use of AMI templates
- Task 1.1- Choose a suitable base AMI (e.g., Amazon Linux 2) that will be used to host the public-facing web application. Install necessary web server software (e.g., Apache or NGINX) and security updates.
- Task 1.2- Select a base AMI for database servers (like Amazon Linux server) and install the database software.
- Task 1.3- After configuring the web and database servers, create custom AMIs from these instances to be used in launching new instances.

2. Dealing with AWS SSH Keys
- Task 2.1- Generate an SSH key pair through the AWS Management Console for secure access to EC2 instances.
- Task 2.2- When launching EC2 instances, specify the generated SSH key pair to allow secure remote access.

3. Networking Configuration
- Task 3.1- Create a new VPC with a custom CIDR block that fits the network architecture.
- Task 3.2- Create public and private subnets within the VPC. Public subnet will host web servers, while the private subnet will host database servers.
- Task 3.3- Attach an Internet Gateway to the VPC and update the route tables to allow outbound traffic from the public subnet.
- Task 3.4- Set up route tables to control traffic flow. The public subnet’s route table should include a route to the Internet Gateway, while the private subnet’s route table should only allow internal communication.

4. Security Group Configuration
- Task 4.1- Define a Security Group that allows HTTP (port 80) and HTTPS (port 443) traffic from the internet and restricts SSH access to specific IP addresses.
- Task 4.2- Define a Security Group for the database server that only allows incoming traffic from the web server’s Security Group on the database port (e.g., MySQL on port 3306).
- Task 4.3- When launching instances, assign the appropriate Security Group (web server for public subnet and database server for private subnet) to each instance.

5. AWS Web Application Firewall (WAF_ Configuration)
- Task 5.1- Define WAF rules that filter incoming web traffic to block common attacks like SQL injection and XSS.
- Task 5.2- If using an Application Load Balancer (ALB), associate the WAF with the ALB to filter incoming requests before they reach the web servers, which enhances the security of the web application by filtering traffic at the load balancer level.
     - Reference: [WAF and ALB Integration](https://docs.aws.amazon.com/waf/latest/developerguide/waf-regional-alb.html)
- Task 5.3- Enable logging for WAF to monitor the types of requests being blocked or allowed.

6. AWS Firewall Manager Configuration
- Task 6.1- Configure AWS Firewall Manager to manage security policies across all accounts within my organization.
- Task 6.2- Define firewall policies for Security Groups, NACLs, and WAF using Firewall Manager. Apply these policies across the appropriate AWS accounts and resources.
- Task 6.3- Regularly monitor the effectiveness of the policies through AWS Firewall Manager and adjust them as needed.
