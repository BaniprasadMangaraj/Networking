
# ☁️ **AWS EC2 & Security Groups**

## 📌 **Overview**
Amazon EC2 (Elastic Compute Cloud) lets you run virtual servers (called instances) on the AWS cloud. Security Groups are like virtual firewalls that help you control what kind of traffic can go **in and out** of your EC2 instances.

---

## 🖥️ **How to Launch an EC2 Instance on AWS**

### ✅ **Step-by-Step Guide**

1. **Login to AWS Console**  
   Go to [https://aws.amazon.com](https://aws.amazon.com) and sign in.

2. **Open EC2 Dashboard**  
   Find “EC2” in the Services menu and click it.

3. **Click “Launch Instance”**  
   Start a new instance.

4. **Choose an Amazon Machine Image (AMI)**  
   - Example: Ubuntu, Amazon Linux, or Windows.
   - These are pre-configured OS templates.

5. **Select Instance Type**  
   - Choose based on your needs (CPU, RAM).  
   - Example: `t2.micro` (free-tier eligible).

6. **Configure Instance Details**  
   - Set number of instances, VPC/network, IAM roles (optional), etc.

7. **Add Storage**  
   - Use the default or increase EBS volume size if needed.

8. **Add Tags** (Optional)  
   - Example: Name = MyDevServer

9. **Configure Security Group**  
   - Create a new one or select an existing group.
   - Add rules for **SSH**, **HTTP**, etc.

10. **Create / Select Key Pair**  
   - Create a new key pair (`.pem`) and download it.  
   - You'll use this key to connect securely using SSH.

11. **Launch the Instance**  
   - Click **Launch**, and wait a few minutes for the instance to be ready.

---

## 🚀 **Connect to Your EC2 Instance (Linux/Ubuntu Example)**

```bash
ssh -i your-key.pem ec2-user@your-ec2-public-ip
```

- Make sure the `.pem` file has the correct permission:
```bash
chmod 400 your-key.pem
```

---

## 🔐 **Understanding Security Groups**

### ✅ What is a Security Group?
- A **Security Group** is like a door policy — it controls who can talk to your instance and on which port.
- It works at the **instance level**, not the whole network.

### ✅ Default Behavior
- **Inbound:** Deny everything by default. You must allow specific ports.
- **Outbound:** Allow all traffic by default (can be modified).

---

## ⚙️ **Common Security Group Rules**

| Purpose            | Protocol | Port(s)     | Source            | Notes                                      |
|--------------------|----------|-------------|--------------------|--------------------------------------------|
| **SSH (Linux)**    | TCP      | 22          | Your IP            | Used for remote login via terminal         |
| **RDP (Windows)**  | TCP      | 3389        | Your IP            | For remote desktop to Windows instances    |
| **HTTP**           | TCP      | 80          | 0.0.0.0/0          | Public web traffic (insecure)              |
| **HTTPS**          | TCP      | 443         | 0.0.0.0/0          | Secure web traffic                         |
| **MySQL**          | TCP      | 3306        | Specific IP only   | Never open this to the public              |
| **PostgreSQL**     | TCP      | 5432        | Specific IP only   | Restrict database access                   |

🛡️ **Tip:** Never allow SSH/RDP access from **Anywhere (0.0.0.0/0)** in production. Use **My IP** or a trusted range only.

---

## 🧠 **Real-World Analogy**

> Imagine your EC2 instance as a **house**, and **Security Groups** are the **doors and locks**:
- You decide **who** can come in (inbound) and **what** can go out (outbound).
- Ports = **doors** to different rooms (22 for SSH, 80 for websites, etc.)

---

## 📚 **Helpful Resources**
- 🔗 [AWS EC2 Docs](https://docs.aws.amazon.com/ec2/)
- 🔗 [Security Groups Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-groups.html)
- 🔗 [Best Practices for Security Groups](https://aws.amazon.com/premiumsupport/knowledge-center/best-practices-security-groups/)
- 🔗 [How SSH Works](https://www.ssh.com/academy/ssh)

---

## 🏁 **Conclusion**
Launching an EC2 instance is like starting your own virtual computer in the cloud. But just like a real computer, you need to protect it. That’s where **Security Groups** come in — they keep your server safe by only letting the right people in. As a DevOps engineer, it's crucial to configure them correctly to avoid security risks.
