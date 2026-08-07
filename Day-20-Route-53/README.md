<p align="center">
  <img src="https://img.shields.io/badge/AWS-Route 53-blueviolet" alt="AWS Badge">
</p>

# ☁ Day 20 – Amazon Route 53 + Custom Domain + CloudFront + UI Upgrade

---

##  Objective

- Configure DNS using Route 53
- Connect custom domain to AWS hosted website
- Enable HTTPS using ACM
- Use CloudFront CDN for global delivery
- Upgrade frontend UI

---

##  Services Used

- Amazon S3
- Amazon CloudFront
- Amazon Route 53
- AWS Certificate Manager (ACM)

---

##  Architecture

<img width="322" height="472" alt="53 drawio" src="https://github.com/user-attachments/assets/55a1df12-e762-498b-ae8d-614962d3db3e" />

---

##  Step 1 – Domain Setup

- Purchased domain: `shashanktj.com`
- Configured nameservers in domain provider (Hostinger)
- Updated nameservers to Route 53

---

##  Step 2 – Hosted Zone Creation

- Created Hosted Zone in Route 53
- Verified NS and SOA records
- Domain successfully linked with AWS

---

##  Step 3 – SSL Certificate (ACM)

- Region used: **us-east-1 (mandatory for CloudFront)**
- Requested public certificate
- Added domains:
  - `shashanktj.com`
  - `www.shashanktj.com`
- Validation method: DNS

### Validation Process

- Created CNAME records in Route 53
- Certificate status:
  - Pending → Issued

---

##  Step 4 – CloudFront Setup

- Created CloudFront distribution
- Origin: S3 static website endpoint
- Viewer protocol policy: Redirect HTTP → HTTPS
- Attached SSL certificate
- Added custom domain

### Important Configurations

- Default root object: `index.html`
- WAF: Disabled

---

##  Step 5 – Route 53 Record Configuration

- Record Type: A
- Alias: Enabled
- Target: CloudFront distribution

### Issue Faced

Error:
"A record with the specified name already exists"

### Solution

- Edited existing A record instead of creating new
- Updated record to point to CloudFront

---

##  Step 6 – UI Upgrade

- Updated `index.html`
- Implemented:
  - Dark theme
  - Modern UI design
  - Responsive layout
  - Sections:
    - About
    - Skills
    - Projects
    - Contact

---

##  Step 7 – CloudFront Invalidation

- Created invalidation to refresh cache:

- Ensured latest UI changes reflect on website

---

##  Screenshots

### 🔹 Route 53 Hosted Zone

### 🔹 SSL Certificate Issued

### 🔹 CloudFront Distribution

### 🔹 Final Website Output

---

##  Final Output

- Website successfully hosted on:
  👉 https://shashanktj.com

- HTTPS enabled   
- CloudFront CDN active  
- UI upgraded   

---

##  Key Learnings

- Route 53 manages DNS routing
- CloudFront improves performance and scalability
- ACM certificates must be created in **us-east-1**
- DNS propagation takes time
- Existing DNS records should be modified, not duplicated
- CloudFront caching requires invalidation after updates

---

##  Challenges Faced

| Issue | Solution |
|------|--------|
| Certificate pending | Fixed using correct CNAME records |
| DNS propagation delay | Waited for sync |
| Duplicate A record error | Edited existing record |
| Website not updating | Used CloudFront invalidation |

---

##  Conclusion

Successfully deployed a production-ready static website using AWS services with:

- Custom domain integration
- Secure HTTPS communication
- Global content delivery using CloudFront
- Improved UI for better user experience

This project demonstrates real-world cloud architecture and practical AWS implementation.

---

##  Next Step

- Add Visitor Counter (Lambda + DynamoDB)
- Integrate API Gateway
- Implement CI/CD pipeline
