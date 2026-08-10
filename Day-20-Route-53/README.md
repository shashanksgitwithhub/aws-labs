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

- Route 53 Dashboard
  <img width="1919" height="1017" alt="Screenshot 2026-08-07 125724" src="https://github.com/user-attachments/assets/3deeff94-6bbe-4e2d-a0b8-d1a8eb8305fb" />
  
- Hosted Zone
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 125936" src="https://github.com/user-attachments/assets/b3519801-7463-4e79-a6ae-f9f230b2351b" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 130009" src="https://github.com/user-attachments/assets/907dbbaf-a8f2-4f62-b2e6-008de87198fd" />
  
- Name servers
  <img width="1919" height="1019" alt="Screenshot 2026-08-07 130653" src="https://github.com/user-attachments/assets/eedd3fe6-0c41-4461-84be-0ae73b47e8e8" />
  
- Bucket Creation
  <img width="1919" height="1019" alt="Screenshot 2026-08-07 130953" src="https://github.com/user-attachments/assets/a350dce0-f435-4411-8cc1-6587485a957e" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-07 131115" src="https://github.com/user-attachments/assets/a717aef5-533b-46ce-bf9f-9a1da5421628" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-07 131135" src="https://github.com/user-attachments/assets/e4174588-1adf-43e0-bf4c-ae757d5b0c09" />
  
- Upload to Bucket
  <img width="1919" height="1017" alt="Screenshot 2026-08-07 131614" src="https://github.com/user-attachments/assets/fb0d9218-5d9f-4ea9-ac0e-7651854d3864" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 131635" src="https://github.com/user-attachments/assets/addb9004-2e7b-4c86-9f19-39d19904f1e8" />
  
- Bucket Policy
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 131804" src="https://github.com/user-attachments/assets/9aaa86dd-9fb9-41a6-a933-316911db0a54" />
  <img width="1919" height="1017" alt="Screenshot 2026-08-07 131833" src="https://github.com/user-attachments/assets/dd4367d7-d228-42ff-8c28-66886032a805" />
  
- Create Record
  <img width="1917" height="1019" alt="Screenshot 2026-08-07 132738" src="https://github.com/user-attachments/assets/1bccb061-4106-42e7-9b1f-7118314bb293" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 132819" src="https://github.com/user-attachments/assets/aab52c13-9755-4943-aa0c-e1050ca9b934" />

- AWS Cretificate Manager Dashboard
  <img width="1919" height="1017" alt="Screenshot 2026-08-07 140039" src="https://github.com/user-attachments/assets/5a412e1b-f5e2-4751-acdd-6cd01195532b" />
  <img width="1919" height="1020" alt="Screenshot 2026-08-07 140118" src="https://github.com/user-attachments/assets/678fc633-f42e-41a8-874d-5775b586c262" />

- Request certificate
  <img width="1919" height="1020" alt="Screenshot 2026-08-07 140152" src="https://github.com/user-attachments/assets/62f5cfc3-580f-406e-9850-36929247f096" />
  <img width="1919" height="1020" alt="Screenshot 2026-08-07 140256" src="https://github.com/user-attachments/assets/bc787938-3186-4c65-8353-ecd1dc8d8da4" />
  <img width="1919" height="1017" alt="Screenshot 2026-08-07 140303" src="https://github.com/user-attachments/assets/65c5ae75-8518-497c-b884-2f9cc61ce59c" />
  <img width="1919" height="1021" alt="Screenshot 2026-08-07 140337" src="https://github.com/user-attachments/assets/47bfd955-5888-4392-85d0-0362a8d443fc" />
  <img width="1919" height="1016" alt="Screenshot 2026-08-07 142120" src="https://github.com/user-attachments/assets/3b749022-c7f1-463f-a3e8-989c93b9becb" />
  <img width="1919" height="1017" alt="Screenshot 2026-08-07 142156" src="https://github.com/user-attachments/assets/ef3b4d7c-7434-495e-8a8c-4b07fbc451e8" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 142828" src="https://github.com/user-attachments/assets/5d02bf55-70c9-4017-a4d5-bdba2b169e24" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-07 150935" src="https://github.com/user-attachments/assets/763878be-fff4-45e4-8696-987ec7ada11c" />
  
- Amazon Cloudfront  Dashboard
  <img width="1918" height="1018" alt="Screenshot 2026-08-07 151331" src="https://github.com/user-attachments/assets/40af5894-c07b-43a9-87bc-3de6eb118af8" />
- Configuration
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 152021" src="https://github.com/user-attachments/assets/695023ae-d32e-4a31-819c-89633f08252f" />
  <img width="1919" height="1016" alt="Screenshot 2026-08-07 152039" src="https://github.com/user-attachments/assets/7cab8017-fa4f-422f-a57d-4a598553f567" />
  <img width="1918" height="1016" alt="Screenshot 2026-08-07 152309" src="https://github.com/user-attachments/assets/55e962bf-3b0a-43d5-a282-a23b4b3e5097" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-07 153003" src="https://github.com/user-attachments/assets/4cd165c6-f5c3-408e-baaa-6e31faf164c4" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-07 154321" src="https://github.com/user-attachments/assets/cd4d18b3-c5ac-439b-9f8c-7257a90e7f5e" />
  <img width="1919" height="1017" alt="Screenshot 2026-08-07 154536" src="https://github.com/user-attachments/assets/e4557f7d-783d-44b3-bf73-fb3e6d4456a7" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 154545" src="https://github.com/user-attachments/assets/96854d49-7a11-4c38-9ccc-6556d6056ae5" />
  <img width="1919" height="1020" alt="Screenshot 2026-08-07 160759" src="https://github.com/user-attachments/assets/9f1d793d-6904-49ad-aeb9-60bb4bd952e1" />
  <img width="1919" height="1020" alt="Screenshot 2026-08-07 161621" src="https://github.com/user-attachments/assets/8b05a9ca-19fe-45e2-8e74-573867ae3935" />
- Website Hosted
  <img width="1919" height="1018" alt="Screenshot 2026-08-07 161640" src="https://github.com/user-attachments/assets/b1fc782e-d56c-4b96-af3f-76aa4abef043" />

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
