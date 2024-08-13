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
More detailed plan based on my diagram:
1. AWS Firewall Manager ("Firewall")
   - Role: Centralized Security Policy Management System
   - Purpose: Manages and enforces firewall rules across all AWS security services, ensuring consistent protection across the cloud environment. 

2. Network Access Control Lists (NACLs):
   - Role: Subnet-Level Traffic Control System
   - Purpose: Adds a layer of security at the subnet level, controlling inbound and outbound traffic by allowing or denying specific IP addresses, protocols, and ports;   
     ensure that unauthorized traffic does not reach your internal resources within the VPC.

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
   - Purpose: Represents the flow of data entering and leaving the subnets and instances. This traffic is managed and filtered by Security Groups, NACLs, and the WAF to ensure that only authorized traffic reaches your AWS resources, maintaining the integrity and security of the environment.
