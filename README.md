
## CI/CD Workflow Using Jenkins and GitHub Webhooks

This project demonstrates a simple and practical CI/CD pipeline using **Jenkins**, **GitHub Webhooks**, and **Linux servers**.

### Architecture Overview

* **Jenkins Server**
  Used for automation, build, and deployment tasks.

* **Live Server (Web Server)**
  Hosts the actual website and serves the HTML files using a web server (Apache/Nginx).

* **GitHub Repository**
  Contains the website source code (`.html` files).

---

### Workflow Explanation

1. **Code Push to GitHub**
   Any change pushed to a specific branch in the GitHub repository triggers a webhook event.
   

3. **GitHub Webhook → Jenkins**
   The webhook notifies the Jenkins server whenever changes are made to the configured branch.

4. **Jenkins Job Execution**
   After receiving the webhook:
    <img width="1920" height="1008" alt="Screenshot 2026-01-01 184600" src="https://github.com/user-attachments/assets/ceaea144-b016-4be2-bbb3-3e754c9cf12f" />

   * Jenkins clones the latest version of the repository.
   * The build process starts automatically.
     <img width="960" height="504" alt="image" src="https://github.com/user-attachments/assets/46ebca58-6105-4ba2-aa2c-13c997b75cdb" />
    <img width="960" height="504" alt="image" src="https://github.com/user-attachments/assets/97398824-a211-44f8-a8c0-d3d43025461c" />



5. **Build Step (Packaging)**

   * Jenkins searches for all files ending with `.html`.
   * These files are compressed into a single ZIP file.
  

zip staticpage.zip ./*.html
sudo scp -i /var/lib/jenkins/.ssh/<keypair>.pem -o StrictHostKeyChecking=no staticpage.zip  ubuntu@54.226.47.55:.
sudo ssh -i /var/lib/jenkins/.ssh/<keypair>.pem -o StrictHostKeyChecking=no ubuntu@54.226.47.55 <<EOF
cd /var/www/html/

sudo rm -rf *
sudo unzip /home/ubuntu/staticpage.zip
curl localhost:80
EOF


6. **Transfer to Live Server**

   * Jenkins securely copies (`scp`) the ZIP file to the live server using SSH authentication.

7. **Deployment on Live Server**

   * Jenkins connects to the live server via SSH.
   * Existing files in `/var/www/html` are removed.
   * The ZIP file is extracted in `/var/www/html`.

8. **Website Update**

   * The live server immediately serves the updated HTML files.
   * No manual intervention is required.
  <img width="1920" height="1008" alt="Screenshot 2026-01-01 184334" src="https://github.com/user-attachments/assets/001749a3-16b2-4f72-9cd2-a252babadb98" />


