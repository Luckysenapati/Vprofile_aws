The **vProfile** project is an AWS-based application designed to manage user access requests to a website. The architecture leverages several AWS services to ensure efficient handling of these requests while maintaining security and scalability.

### Architecture Overview

1. **User Request Handling**: Users initiate access requests via HTTP or HTTPS, which are directed to an **AWS Application Load Balancer (ALB)**. This load balancer is configured under a security group named **vprofile-ELB_SG**.

2. **Request Routing**: The ALB forwards incoming requests to **Tomcat instances** that are part of an **Auto Scaling Group**. These instances operate under another security group, **vprofile-app-sg**, ensuring that only authorized traffic reaches them.

3. **Integration with S3 and Route 53**: The Auto Scaling Group is connected to an **S3 bucket** for storage purposes and utilizes **Amazon Route 53** to manage DNS within a private zone for backend instances.

4. **Backend Processing**: After passing through the application layer, requests reach the backend, which consists of three instances—**MySQL**, **RabbitMQ**, and **Memcached**—all secured under a single security group called **vprofile-backend-sg**. These components work together to process and deliver the requested data to users.

### Execution Flow

The setup and deployment process for the vProfile project follows these steps:

1. **Login to AWS Account**: Access the AWS Management Console.

2. **Create Key Pairs**: Generate key pairs for secure access to EC2 instances.

3. **Create Security Groups**: Define security groups to control inbound and outbound traffic.

4. **Launch Instances with User Data**: Deploy EC2 instances using user data scripts written in Bash.

5. **Update IP to Name Mapping in Route 53**: Configure DNS settings to ensure proper routing of traffic.

6. **Build Application from Source Code**: Compile the application code necessary for deployment.

7. **Upload to S3 Bucket**: Store the application artifacts in an S3 bucket for easy access.

8. **Download Artifact to Tomcat EC2 Instance**: Transfer the application files to the Tomcat server.

9. **Setup ELB with HTTPS**: Configure the Application Load Balancer to handle HTTPS traffic, utilizing certificates from **AWS Certificate Manager**.

10. **Map ELB Endpoint to Website Name in GoDaddy DNS**: Link the load balancer's endpoint to a domain name registered with GoDaddy.

11. **Verify**: Test the setup to ensure everything is functioning correctly.

12. **Build Auto Scaling Group for Tomcat Instances**: Implement auto scaling to manage traffic loads dynamically.

This comprehensive architecture and execution plan enable vProfile to efficiently manage user requests while ensuring high availability and security. The project exemplifies the use of AWS services to create a robust web application infrastructure.
