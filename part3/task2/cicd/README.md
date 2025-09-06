## **DevOps CI/CD Pipeline for Java Web App**

### **Overview**
This project automates the Continuous Integration and Continuous Delivery (CI/CD) process for a Java web application using a Declarative Jenkins Pipeline. The pipeline is designed to be robust and secure, integrating various industry-standard tools to ensure high-quality, reliable, and consistent deployments.

### **Pipeline Stages**

The pipeline is structured into several key stages to ensure a smooth and automated workflow. 

#### **1. Git Checkout**
- **Purpose:** Fetches the latest code from the specified Git repository.
- **Details:** The pipeline checks out the `main` branch from a GitLab repository using a predefined credential.

#### **2. Build**
- **Purpose:** Compiles the source code and packages it into an executable artifact.
- **Details:** Uses Maven to perform a clean build and package the application into a `.war` file, skipping tests at this stage for faster compilation. The resulting `.war` file is then archived as a build artifact.

#### **3. Test**
- **Purpose:** Runs unit and integration tests to validate the application's integrity.
- **Details:** Executes the Maven `test` goal to run all tests defined in the project.

#### **4. OWASP Scan**
- **Purpose:** Analyzes the project's dependencies for known vulnerabilities.
- **Details:** Uses the **OWASP Dependency-Check** tool to generate a security report, helping to identify and mitigate potential risks early in the development cycle.

#### **5. Checkstyle Analysis**
- **Purpose:** Enforces coding standards and style conventions.
- **Details:** Runs Maven's Checkstyle plugin to ensure the codebase adheres to predefined formatting rules, promoting consistency and maintainability.

#### **6. SonarQube Analysis**
- **Purpose:** Performs static code analysis to measure code quality and identify bugs, vulnerabilities, and code smells.
- **Details:** The pipeline sends the source code to a SonarQube server for a detailed analysis. It also includes JaCoCo and Surefire reports for code coverage and test results.

#### **7. Quality Gate**
- **Purpose:** Ensures the code meets a minimum quality standard before proceeding.
- **Details:** The pipeline waits for a response from the SonarQube server's Quality Gate. If the quality criteria are not met, the pipeline is aborted, preventing low-quality code from being deployed.

#### **8. Upload Artifact to Nexus**
- **Purpose:** Publishes the built `.war` artifact to a centralized repository.
- **Details:** Uploads the application artifact to a Nexus repository, which acts as a single source of truth for all dependencies and build outputs.

#### **9. Build Docker**
- **Purpose:** Creates a Docker image of the application.
- **Details:** A Docker image is built from the application and tagged for consistency. This image encapsulates the application and its dependencies, ensuring it runs reliably in any environment.

#### **10. Trivy Image Scan**
- **Purpose:** Scans the newly created Docker image for security vulnerabilities.
- **Details:** Uses the Trivy security scanner to check the Docker image for known vulnerabilities in its OS packages and application dependencies.

#### **11. Docker Push**
- **Purpose:** Publishes the Docker image to a container registry.
- **Details:** The pipeline logs in to Docker Hub using stored credentials and pushes the newly built and scanned Docker image. It also cleans up the local Jenkins workspace by removing old Docker images.

#### **12. Azure Login**
- **Purpose:** Authenticates with the Azure cloud platform.
- **Details:** Uses a service principal to securely log into Azure, preparing for subsequent infrastructure provisioning and deployment.

#### **13. Provision AKS Cluster**
- **Purpose:** Creates or updates a Kubernetes cluster in Azure.
- **Details:** Executes Terraform scripts to provision an Azure Kubernetes Service (AKS) cluster, demonstrating **Infrastructure as Code (IaC)**. This stage ensures a consistent and repeatable environment for deployment.

#### **14. Deploy App on EKS**
- **Purpose:** Deploys the application to the Kubernetes cluster.
- **Details:** Uses `kubectl` to apply the Kubernetes manifests from a dedicated directory, deploying the application's Docker image onto the provisioned AKS cluster.

### **Notifications**
- **Purpose:** Provides real-time status updates on the pipeline's execution.
- **Details:** Upon completion of the pipeline (regardless of success or failure), an automated notification is sent to a specified Slack channel, informing the team about the build status, job name, and a link to the build log.