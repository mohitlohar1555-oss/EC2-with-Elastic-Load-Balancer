<h2>📌 Project Overview</h2>

<p>
This project demonstrates how to deploy multiple Amazon EC2 instances
behind an Application Load Balancer (ALB).
The Load Balancer receives incoming user requests and distributes
traffic across healthy EC2 instances.
</p>

<p>
The architecture uses Security Groups, EC2 instances, Target Groups,
health checks and an Application Load Balancer.
</p>

<div class="flow">

👤 User
&nbsp; → &nbsp;
⚖️ Load Balancer
&nbsp; → &nbsp;
🎯 Target Group
&nbsp; → &nbsp;
🖥️ EC2 Instances

</div>

</section>


<!-- INTRODUCTION -->

<section>

<h2>📖 Introduction</h2>

<p>
A Load Balancer is a service that distributes incoming network traffic
across multiple servers such as EC2 instances.
</p>

<p>
It helps provide:
</p>

<ul>
    <li>High availability</li>
    <li>Reliability</li>
    <li>Better performance</li>
    <li>Traffic distribution</li>
    <li>Fault tolerance</li>
</ul>

<p>
The Load Balancer can route traffic to healthy servers and avoid
unhealthy targets.
</p>

</section>


<!-- WHY ELB -->

<section>

<h2>⚖️ What is ELB?</h2>

<p>
<strong>ELB</strong> stands for <strong>Elastic Load Balancing</strong>.
It is an AWS service that distributes incoming traffic across
multiple registered targets.
</p>

<h3>Why is ELB used?</h3>

<ul>
    <li>To distribute incoming traffic</li>
    <li>To improve availability</li>
    <li>To prevent a single server from handling all requests</li>
    <li>To route traffic to healthy instances</li>
    <li>To improve reliability</li>
    <li>To support scalable architectures</li>
</ul>

<div class="architecture">

                USERS
                  |
                  v
          +---------------+
          |     ELB       |
          | Load Balancer |
          +-------+-------+
                  |
          +-------+-------+
          |       |       |
          v       v       v
        EC2-1   EC2-2   EC2-3

</div>

</section>


<!-- ALB -->

<section>

<h2>🔄 What is Application Load Balancer?</h2>

<p>
For this project, an <strong>Application Load Balancer (ALB)</strong>
is used.
</p>

<p>
ALB is designed for application traffic such as HTTP and HTTPS.
It receives requests from users and forwards them to registered
healthy targets.
</p>

</section>


<!-- PREREQUISITES -->

<section>

<h2>📝 Prerequisites</h2>

<p>Before starting the project, you should have:</p>

<div class="card-container">

<div class="card">
<h3>☁️ AWS Account</h3>
<p>
An AWS account is required to create EC2 instances,
Security Groups, Target Groups and Load Balancers.
</p>
</div>

<div class="card">
<h3>🧠 AWS Knowledge</h3>
<p>
Basic knowledge of EC2, Security Groups,
Target Groups and Load Balancing.
</p>
</div>

<div class="card">
<h3>🌐 Internet</h3>
<p>
Internet access is required to access the AWS Management Console.
</p>
</div>

</div>

</section>


<!-- SECURITY GROUP -->

<section>

<h2>🔐 1. Security Group</h2>

<p>
A Security Group acts as a virtual firewall that controls
inbound and outbound traffic.
</p>

<p>
In this project, the Security Group is used to protect
the Load Balancer and EC2 instances.
</p>

<h3>Example Inbound Rules</h3>

<table>

<tr>
<th>Protocol</th>
<th>Port</th>
<th>Purpose</th>
</tr>

<tr>
<td>SSH</td>
<td>22</td>
<td>Secure administration</td>
</tr>

<tr>
<td>HTTP</td>
<td>80</td>
<td>Web traffic</td>
</tr>

<tr>
<td>HTTPS</td>
<td>443</td>
<td>Secure web traffic</td>
</tr>

</table>

<h3>Role of Security Group</h3>

<p>
<strong>
Protects the Load Balancer and EC2 instances by allowing
only required traffic.
</strong>
</p>

</section>


<!-- EC2 -->

<section>

<h2>🖥️ 2. EC2 Instance</h2>

<p>
<strong>EC2 (Elastic Compute Cloud)</strong> provides virtual
servers in AWS.
</p>

<p>
In this project, EC2 instances host and run the application.
The Load Balancer distributes user requests to these instances.
</p>

<h3>Role of EC2</h3>

<p>
<strong>Hosts and runs the application.</strong>
</p>

<div class="architecture">

              LOAD BALANCER
                    |
          +---------+---------+
          |         |         |
          v         v         v
       EC2-01    EC2-02    EC2-03

</div>

</section>


<!-- USER DATA -->

<section>

<h2>⚙️ What is EC2 User Data?</h2>

<p>
EC2 User Data allows commands or scripts to be provided
when launching an EC2 instance.
It is commonly used to automate the initial configuration
of the instance.
</p>

<h3>Why use User Data?</h3>

<ul>
    <li>Automate server configuration</li>
    <li>Install required software</li>
    <li>Configure services</li>
    <li>Start services automatically</li>
</ul>

<h3>Example</h3>

<pre>
#!/bin/bash

# Example initialization commands

echo "EC2 instance initialized"
</pre>

<div class="warning">

<strong>Note:</strong>
The exact User Data script depends on the operating system
and application requirements.

</div>

</section>


<!-- TARGET GROUP -->

<section>

<h2>🎯 3. Target Group</h2>

<p>
A Target Group is a collection of registered targets.
In this project, the targets are EC2 instances.
</p>

<p>
The Target Group performs health checks and helps ensure
that the Load Balancer sends traffic to healthy instances.
</p>

<h3>Role</h3>

<p>
<strong>
Groups EC2 instances and monitors their health.
</strong>
</p>

<div class="architecture">

             TARGET GROUP
            /      |      \
           /       |       \
          v        v        v
       EC2-01   EC2-02   EC2-03

</div>

</section>


<!-- HEALTH CHECK -->

<section>

<h2>❤️ What is a Health Check?</h2>

<p>
A health check determines whether a registered EC2 target
is healthy and able to receive traffic.
</p>

<pre>
EC2-01 → Healthy ✅
EC2-02 → Healthy ✅
EC2-03 → Unhealthy ❌
</pre>

<p>
Traffic should be sent only to healthy instances.
</p>

<div class="success">

<strong>Healthy Targets:</strong>

EC2-01 and EC2-02 can receive traffic.

<br><br>

<strong>Unhealthy Target:</strong>

EC2-03 should not receive new traffic while unhealthy.

</div>

</section>


<!-- LOAD BALANCER -->

<section>

<h2>⚖️ 4. Load Balancer (ALB)</h2>

<p>
The Application Load Balancer receives incoming user requests
and distributes them across healthy EC2 instances.
</p>

<h3>Role</h3>

<p>
<strong>
Distributes incoming traffic to healthy EC2 instances,
helping provide high availability, scalability and fault tolerance.
</strong>
</p>

</section>


<!-- ARCHITECTURE -->

<section>

<h2>🏗️ Complete Architecture</h2>

<div class="architecture">

                         USERS
                           |
                           v
                   +---------------+
                   | Load Balancer |
                   |     (ALB)     |
                   +-------+-------+
                           |
                           v
                    +-------------+
                    | Target Group|
                    +------+------+ 
                           |
             +-------------+-------------+
             |             |             |
             v             v             v
          EC2-01        EC2-02        EC2-03
         Healthy       Healthy      Unhealthy
             |             |
             +------+------+
                    |
                    v
            Traffic sent only
            to healthy instances

             SECURITY GROUP
                    |
        Protects Load Balancer
                    +
              EC2 Instances

</div>

</section>


<!-- SETUP -->

<section>

<h2>🏗️ Steps to Set Up the Infrastructure</h2>


<div class="step">

<div class="step-number">STEP 1 — Configure Security Group</div>

<p>
Go to the AWS Management Console.
</p>

<p>
Search for and open <strong>EC2</strong>.
</p>

<p>
Select <strong>Security Groups</strong>.
</p>

<p>
Click <strong>Create Security Group</strong>.
</p>

</div>


<div class="step">

<div class="step-number">STEP 2 — Enter Security Group Details</div>

<p>
Enter the Security Group name and description.
</p>

<p>
Configure the required inbound rules.
</p>

<ul>
    <li>SSH — Port 22</li>
    <li>HTTP — Port 80</li>
    <li>HTTPS — Port 443</li>
</ul>

<p>
Select the required source according to your security
requirements.
</p>

<p>
Click <strong>Create Security Group</strong>.
</p>

</div>


<div class="step">

<div class="step-number">STEP 3 — Launch EC2 Instances</div>

<p>
Go to the EC2 Instances Dashboard.
</p>

<p>
Click <strong>Launch Instance</strong>.
</p>

<p>
Provide an instance name.
</p>

<p>
Select the required AMI.
The PPT uses Amazon Linux.
</p>

<p>
Select an appropriate instance type such as
<strong>t2.micro</strong> or <strong>t3.micro</strong>
depending on current AWS availability and eligibility.
</p>

</div>


<div class="step">

<div class="step-number">STEP 4 — Configure Key Pair</div>

<p>
Configure the key pair according to your access requirements.
</p>

<p>
The project PPT shows proceeding without a key pair.
</p>

</div>


<div class="step">

<div class="step-number">STEP 5 — Configure Networking</div>

<p>
In Networking Settings, select the Security Group
created earlier.
</p>

</div>


<div class="step">

<div class="step-number">STEP 6 — Add User Data</div>

<p>
Scroll down to <strong>Advanced Details</strong>.
</p>

<p>
Add the required User Data script.
</p>

<pre>
#!/bin/bash

# Add your initialization commands here

echo "EC2 instance initialized"
</pre>

</div>


<div class="step">

<div class="step-number">STEP 7 — Launch Multiple Instances</div>

<p>
Change the number of instances from 1 to 3.
</p>

<p>
Click <strong>Launch Instance</strong>.
</p>

<p>
Navigate to the EC2 Instances Dashboard and wait
for the instance status checks to pass.
</p>

</div>


<!-- TARGET GROUP SETUP -->

<div class="step">

<div class="step-number">STEP 8 — Create Target Group</div>

<p>
Go to the Load Balancing section.
</p>

<p>
Click <strong>Target Groups</strong>.
</p>

<p>
Click <strong>Create Target Group</strong>.
</p>

</div>


<div class="step">

<div class="step-number">STEP 9 — Configure Target Group</div>

<p>
Enter a Target Group name.
</p>

<p>
Select the available EC2 instances.
</p>

<p>
Register the instances as targets.
</p>

<p>
Review the targets and click
<strong>Create Target Group</strong>.
</p>

</div>


<!-- ALB -->

<div class="step">

<div class="step-number">STEP 10 — Create Elastic Load Balancer</div>

<p>
Go to <strong>Load Balancers</strong> in the Load Balancing section.
</p>

<p>
Click <strong>Create Load Balancer</strong>.
</p>

<p>
Choose:
</p>

<h3>Application Load Balancer (ALB)</h3>

</div>


<div class="step">

<div class="step-number">STEP 11 — Configure ALB</div>

<p>
Enter the Load Balancer name.
</p>

<p>
Configure the required Availability Zones and subnets.
</p>

<p>
Remove the default Security Group if required and
attach the Security Group created earlier.
</p>

</div>


<div class="step">

<div class="step-number">STEP 12 — Configure Listener and Routing</div>

<p>
In <strong>Listeners and Routing</strong>,
attach the Target Group created earlier.
</p>

<p>
The listener receives incoming traffic and forwards it
to the Target Group.
</p>

</div>


<div class="step">

<div class="step-number">STEP 13 — Create Load Balancer</div>

<p>
Review the configuration.
</p>

<p>
Click <strong>Create Load Balancer</strong>.
</p>

<p>
Wait until the ELB status becomes <strong>Active</strong>.
</p>

</div>


<!-- TESTING -->

<div class="step">

<div class="step-number">STEP 14 — Test the Load Balancer</div>

<p>
Copy the Load Balancer DNS name.
</p>

<p>
Open an incognito browser window.
</p>

<p>
Paste the Load Balancer DNS name into the browser.
</p>

</div>


<div class="step">

<div class="step-number">STEP 15 — Verify Traffic Distribution</div>

<p>
Refresh the browser and observe the application response.
</p>

<p>
The Load Balancer can route traffic between the healthy
registered EC2 instances.
</p>

</div>

</section>


<!-- REQUEST FLOW -->

<section>

<h2>🔄 User Request Flow</h2>

<div class="architecture">

                 USER
                   |
                   | HTTP Request
                   v
             LOAD BALANCER
                   |
                   v
              LISTENER
                   |
                   v
             TARGET GROUP
              /    |    \
             /     |     \
            v      v      v
          EC2-1  EC2-2  EC2-3
         HEALTHY HEALTHY UNHEALTHY
            |      |
            +------+
                |
                v
       Traffic sent only to
         healthy instances
                |
                v
             RESPONSE
                |
                v
               USER

</div>

</section>


<!-- WHY EACH SERVICE -->

<section>

<h2>🧠 Why Do We Need Each Component?</h2>

<table>

<tr>
<th>Component</th>
<th>Why We Use It</th>
</tr>

<tr>
<td>Security Group</td>
<td>Controls inbound and outbound traffic.</td>
</tr>

<tr>
<td>EC2</td>
<td>Hosts and runs the application.</td>
</tr>

<tr>
<td>User Data</td>
<td>Automates initial EC2 configuration.</td>
</tr>

<tr>
<td>Target Group</td>
<td>Groups EC2 instances and performs health checks.</td>
</tr>

<tr>
<td>Health Check</td>
<td>Determines whether an EC2 target is healthy.</td>
</tr>

<tr>
<td>Application Load Balancer</td>
<td>Distributes incoming traffic to healthy targets.</td>
</tr>

<tr>
<td>Listener</td>
<td>Receives incoming traffic and forwards it to the Target Group.</td>
</tr>

</table>

</section>


<!-- FAILURE -->

<section>

<h2>❌ What Happens When an Instance Becomes Unhealthy?</h2>

<p>
Suppose EC2-3 becomes unhealthy.
</p>

<pre>
EC2-1 → Healthy ✅
EC2-2 → Healthy ✅
EC2-3 → Unhealthy ❌
</pre>

<p>
The Target Group health check identifies the unhealthy target.
The Load Balancer sends traffic only to the healthy instances.
</p>

<div class="architecture">

                 LOAD BALANCER
                      |
              +-------+-------+
              |               |
              v               v
           EC2-01          EC2-02
          Healthy         Healthy

              X
              |
              v
           EC2-03
         Unhealthy

</div>

</section>


<!-- BENEFITS -->

<section>

<h2>🎯 Benefits of the Project</h2>

<div class="card-container">

<div class="card">
<h3>🔄 Traffic Distribution</h3>
<p>
Incoming requests are distributed across registered
healthy instances.
</p>
</div>

<div class="card">
<h3>❤️ Health Monitoring</h3>
<p>
Target Group health checks identify unhealthy instances.
</p>
</div>

<div class="card">
<h3>🛡️ Security</h3>
<p>
Security Groups control network traffic to the infrastructure.
</p>
</div>

<div class="card">
<h3>📈 Scalability</h3>
<p>
Multiple EC2 instances can participate in the architecture.
</p>
</div>

<div class="card">
<h3>⚡ Availability</h3>
<p>
Traffic can continue through healthy instances when another
instance becomes unhealthy.
</p>
</div>

<div class="card">
<h3>🤖 Automation</h3>
<p>
EC2 User Data can automate initial instance configuration.
</p>
</div>

</div>

</section>


<!-- TROUBLESHOOTING -->

<section>

<h2>🛠️ Troubleshooting</h2>

<h3>Target is Unhealthy ❌</h3>

<ul>
    <li>Check whether the EC2 instance is running.</li>
    <li>Check the application/service on the instance.</li>
    <li>Check Target Group health check configuration.</li>
    <li>Check Security Group rules.</li>
    <li>Check that the EC2 instance is registered with the Target Group.</li>
</ul>

<h3>Load Balancer is Not Working</h3>

<ul>
    <li>Check Load Balancer status.</li>
    <li>Check listener configuration.</li>
    <li>Check Target Group association.</li>
    <li>Check Security Group configuration.</li>
    <li>Check target health.</li>
</ul>

</section>


<!-- PROJECT FLOW -->

<section>

<h2>📋 Complete Project Flow</h2>

<div class="architecture">

1. Create Security Group
          ↓
2. Launch EC2 Instances
          ↓
3. Configure User Data
          ↓
4. Wait for Instance Checks
          ↓
5. Create Target Group
          ↓
6. Register EC2 Instances
          ↓
7. Configure Health Checks
          ↓
8. Create Application Load Balancer
          ↓
9. Select Availability Zones/Subnets
          ↓
10. Attach Security Group
          ↓
11. Attach Target Group
          ↓
12. Create Load Balancer
          ↓
13. Wait for Active Status
          ↓
14. Copy Load Balancer DNS
          ↓
15. Open DNS in Browser
          ↓
16. Test Traffic Distribution

</div>

</section>


<!-- INTERVIEW -->

<section>

<h2>🎤 Interview Explanation</h2>

<p>
<strong>Question: Explain your AWS EC2 Load Balancer project.</strong>
</p>

<p>
<strong>Answer:</strong>
</p>

<p>
"I created an AWS project using multiple EC2 instances,
a Target Group, Security Group and an Application Load Balancer.
First, I created a Security Group to control network traffic.
Then I launched three EC2 instances and configured User Data
during instance creation. After that, I created a Target Group
and registered the EC2 instances. The Target Group performs
health checks to determine which instances are healthy.
Finally, I created an Application Load Balancer, attached the
Security Group, selected the required Availability Zones and
connected the Target Group. I copied the Load Balancer DNS name
and tested it through a browser. The Load Balancer routes traffic
to healthy EC2 instances."
</p>

</section>


<!-- RESUME -->

<section>

<h2>💼 Resume Description</h2>

<p>
<strong>AWS EC2 with Elastic Load Balancer</strong>
</p>

<p>
Designed and implemented an AWS load balancing architecture
using multiple EC2 instances, Application Load Balancer,
Target Group, Security Groups and health checks. Configured
EC2 User Data for instance initialization and tested traffic
routing through the Load Balancer DNS endpoint.
</p>

</section>


<!-- SKILLS -->

<section>

<h2>🧠 Skills Demonstrated</h2>

<div>

<span class="badge">AWS EC2</span>
<span class="badge">Elastic Load Balancing</span>
<span class="badge">Application Load Balancer</span>
<span class="badge">Target Groups</span>
<span class="badge">Security Groups</span>
<span class="badge">Health Checks</span>
<span class="badge">User Data</span>
<span class="badge">AWS Networking</span>
<span class="badge">High Availability</span>
<span class="badge">Cloud Computing</span>
<span class="badge">DevOps</span>

</div>

</section>


<!-- CONCLUSION -->

<section>

<h2>🏁 Conclusion</h2>

<p>
This project demonstrates how EC2 instances, Security Groups,
Target Groups and an Application Load Balancer work together
to distribute traffic across healthy application servers.
</p>

<div class="flow">

👤 User
→ ⚖️ Load Balancer
→ 🎯 Target Group
→ ❤️ Health Check
→ 🖥️ Healthy EC2
→ 🔄 Response
→ 👤 User

</div>

<p>
The project provides practical experience with AWS compute,
network security, load balancing, health monitoring and
cloud infrastructure deployment.
</p>

</section>

</div>


<footer>

<h3>🚀 AWS ELB Project</h3>

<p>Created by <strong>Mohit Gadilohar</strong></p>

<p>
AWS Cloud • EC2 • ALB • Target Group • Security Group
</p>

</footer>

</body>
</html>
