# ⚙️ Maven & Tomcat Installation Guide

Step-by-step installation and configuration scripts for **Apache Maven** and **Apache Tomcat** on Linux — essential DevOps tooling for Java application CI/CD pipelines.

Forked from [keshavr21/installation](https://github.com/keshavr21/installation) and maintained by [Parthasarathy28](https://github.com/Parthasarathy28).

---

## 📌 What's Included

### `maven_installation`
Shell script or notes for installing Apache Maven on a Linux server.

**Steps covered:**
- Download Maven binary from Apache
- - Extract and move to `/opt/maven`
  - - Set `MAVEN_HOME` and update `PATH` in `/etc/profile.d/`
    - - Verify installation with `mvn --version`
     
      - ### `tomcat-users.xml`
      - Configuration file for Apache Tomcat user roles and credentials.
     
      - **What it configures:**
      - - `manager-gui` role for web-based deployment
        - - `admin-gui` role for host management
          - - User credentials for Tomcat Manager UI
           
            - **Use case:** Required for Jenkins to deploy WAR files directly to Tomcat via the Tomcat Deploy plugin.
           
            - ---

            ## 🚀 Quick Installation

            ### Install Maven on Linux (CentOS/Ubuntu)

            ```bash
            # Download Maven
            wget https://downloads.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz

            # Extract
            tar -xzf apache-maven-3.9.6-bin.tar.gz
            sudo mv apache-maven-3.9.6 /opt/maven

            # Set environment variables
            echo 'export MAVEN_HOME=/opt/maven' | sudo tee /etc/profile.d/maven.sh
            echo 'export PATH=$MAVEN_HOME/bin:$PATH' | sudo tee -a /etc/profile.d/maven.sh
            source /etc/profile.d/maven.sh

            # Verify
            mvn --version
            ```

            ### Install Tomcat on Linux

            ```bash
            # Download Tomcat
            wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.87/bin/apache-tomcat-9.0.87.tar.gz

            # Extract
            tar -xzf apache-tomcat-9.0.87.tar.gz
            sudo mv apache-tomcat-9.0.87 /opt/tomcat

            # Set permissions
            sudo chmod +x /opt/tomcat/bin/*.sh

            # Start Tomcat
            /opt/tomcat/bin/startup.sh

            # Verify - open browser at:
            # http://localhost:8080
            ```

            ### Configure Tomcat Users (for Manager access)

            Edit `/opt/tomcat/conf/tomcat-users.xml`:

            ```xml
            <tomcat-users>
              <role rolename="manager-gui"/>
              <role rolename="admin-gui"/>
              <user username="admin" password="admin123"
                    roles="manager-gui,admin-gui"/>
            </tomcat-users>
            ```

            ---

            ## 🔄 CI/CD Integration

            This setup enables Jenkins to automatically deploy WAR files to Tomcat:

            ```
            Jenkins Pipeline:
              1. Git clone → Pull source code
              2. mvn package → Build WAR file
              3. Deploy Plugin → Push WAR to Tomcat Manager
              4. App live at http://server:8080/app
            ```

            ---

            ## 🛠️ Tech Stack

            | Tool | Version | Purpose |
            |---|---|---|
            | Apache Maven | 3.9+ | Java build tool |
            | Apache Tomcat | 9.x / 10.x | Java web server |
            | Linux | Ubuntu/CentOS | OS |
            | Jenkins | LTS | CI/CD orchestration |

            ---

            ## 👤 Author

            **Parthasarathy** — DevOps Engineer | Bengaluru, India
            - GitHub: [@Parthasarathy28](https://github.com/Parthasarathy28)
            - - Email: parthasarathi.paandhaman@gmail.com
              - - Skills: AWS · Kubernetes · Terraform · Jenkins · Docker
               
                - ---

                ## 📄 License

                MIT License
