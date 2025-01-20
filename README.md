Here’s a structured guide for **Lab 4: Configure Load Balancer and Auto Scaling on EC2**:

---

### **Objective**
Set up an application on AWS EC2 instances with a Load Balancer and configure Auto Scaling to manage application availability and scalability.

---

### **Steps to Configure Load Balancer and Auto Scaling on EC2**

#### **1. Prerequisites**
- An AWS account.
- Basic knowledge of EC2, Load Balancer, and Auto Scaling concepts.
- A configured VPC, Subnets, and Security Groups.

---

#### **2. Launch EC2 Instances**
1. **Go to the EC2 Console**:
   - Navigate to the **EC2 Dashboard** in the AWS Management Console.
   - Click on **Launch Instances**.

2. **Choose an AMI**:
   - Use Amazon Linux 2 or any other preferred OS.

3. **Instance Type**:
   - Select an appropriate instance type (e.g., t2.micro for free tier).

4. **Configure Instance Details**:
   - Choose a VPC and Subnet.
   - Enable Auto-assign Public IP.

5. **Add Storage**:
   - Default 8 GiB SSD is sufficient.

6. **Add Tags**:
   - Add a tag for identification (e.g., `Key: Name, Value: WebServer`).

7. **Configure Security Group**:
   - Allow inbound HTTP (port 80) and SSH (port 22).

8. **Launch the Instance**:
   - Select or create a key pair for SSH access.

---

#### **3. Install Web Application on EC2**
1. SSH into the instance using your key pair.
   ```bash
   ssh -i "your-key.pem" ec2-user@<public-ip>
   ```
2. Update and install Apache or Nginx (e.g., for Apache):
   ```bash
   sudo yum update -y
   sudo yum install -y httpd
   ```
3. Start and enable the service:
   ```bash
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```
4. Add a simple HTML file for testing:
   ```bash
   echo "Welcome to Lab 4 - Load Balancer and Auto Scaling!" > /var/www/html/index.html
   ```

---

#### **4. Configure the Load Balancer**
1. **Go to the EC2 Console** > **Load Balancers** > **Create Load Balancer**.
2. **Select Application Load Balancer (ALB)**:
   - Choose the Internet-facing option.
   - Assign the Load Balancer to the same VPC and public subnets.
3. **Configure Security Group**:
   - Allow inbound HTTP traffic (port 80).
4. **Configure Target Group**:
   - Create a new target group (Instance type).
   - Register your EC2 instance.
5. **Configure Listener**:
   - Add a listener for HTTP (port 80) that forwards traffic to the target group.
6. **Review and Create**:
   - Verify settings and create the Load Balancer.

---

#### **5. Configure Auto Scaling**
1. **Go to Auto Scaling Groups** > **Create Auto Scaling Group**.
2. **Define Launch Template**:
   - Create a Launch Template using the same configuration as your running EC2 instance.
3. **Configure Auto Scaling Group**:
   - Assign it to the Load Balancer target group.
   - Set desired, minimum, and maximum instance counts (e.g., 1, 1, and 3).
4. **Define Scaling Policies**:
   - Enable dynamic scaling (e.g., based on CPU utilization).
     - Target Value: 50% CPU utilization.
   - Optionally, enable scheduled scaling for predictable traffic.
5. **Review and Create**:
   - Confirm the settings and create the Auto Scaling group.

---

#### **6. Test the Setup**
1. **Load Balancer**:
   - Access the Load Balancer DNS name (e.g., `http://<Load-Balancer-DNS>`).
   - Verify the web application is served.
2. **Auto Scaling**:
   - Simulate load (e.g., using a load testing tool like Apache Bench).
   - Monitor the creation or termination of instances in the Auto Scaling Group.

---

#### **7. Clean Up Resources**
- Terminate the Auto Scaling Group, Load Balancer, and EC2 instances to avoid additional costs.

---

This hands-on lab demonstrates how to set up a scalable and highly available web application using AWS EC2, Load Balancer, and Auto Scaling.
