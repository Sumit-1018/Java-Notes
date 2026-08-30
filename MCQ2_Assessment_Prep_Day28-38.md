# QuantumCrew — MCQ2 Assessment Prep
### Covering Day 28 – Day 38 (React, DevOps, Cloud/AWS, Git/GitLab, Docker/SonarQube, CI/CD/Jenkins)

> Correct answer is **bolded**.

---
## Day 28 — React Component Lifecycle & Hooks

**Q1.** How many phases does the React class component lifecycle have?
A) 2  B) **3**  C) 4  D) 5

**Q2.** Which phase runs when a component is first created?
A) Updating  B) **Mounting**  C) Unmounting  D) Rendering

**Q3.** Which phase runs when a component is removed from the DOM?
A) Mounting  B) Updating  C) **Unmounting**  D) None of these

**Q4.** Which lifecycle method is required and always called?
A) componentDidMount  B) **render()**  C) componentWillUnmount  D) shouldComponentUpdate

**Q5.** Which lifecycle method is best suited for fetching data from an API?
A) constructor  B) **componentDidMount**  C) render  D) componentWillUnmount

**Q6.** `static getDerivedStateFromProps` is called:
A) Only once ever  B) **On every render**  C) Only on unmount  D) Never automatically

**Q7.** Which method can prevent a re-render by returning `false`?
A) componentDidUpdate  B) **shouldComponentUpdate**  C) getSnapshotBeforeUpdate  D) render

**Q8.** `getSnapshotBeforeUpdate` must be used together with:
A) constructor  B) **componentDidUpdate**  C) render  D) componentWillUnmount

**Q9.** Where is cleanup code (closing connections, destroying objects) typically placed?
A) componentDidMount  B) render  C) **componentWillUnmount**  D) constructor

**Q10.** React Hooks can only be used inside:
A) Class components  B) **Functional components**  C) Any JS file  D) HTML files directly

**Q11.** Which is a rule for using Hooks?
A) Can be used in loops  B) Can be called conditionally  C) **Must be called at the top level**  D) Only one hook allowed per component

**Q12.** `useState` returns:
A) Only the current value  B) **The current state and an updater function**  C) A Promise  D) Nothing

**Q13.** Which hook performs side effects like fetching data or updating the DOM?
A) useState  B) **useEffect**  C) useRef  D) useContext

**Q14.** `useEffect(fn, [])` behaves like which class lifecycle method?
A) componentDidUpdate  B) **componentDidMount**  C) componentWillUnmount  D) render

**Q15.** Which hook is recommended for managing complex state logic?
A) useState  B) useRef  C) **useReducer**  D) useContext

**Q16.** With no dependency array at all, `useEffect` runs:
A) Only once  B) **On every render**  C) Never  D) Only on unmount

---
## Day 29 — DevOps & Cloud Computing Fundamentals

**Q1.** DevOps combines which two areas?
A) Design + Testing  B) **Development + Operations**  C) Data + Ops  D) Development + Deployment only

**Q2.** In the described DevOps flow, what comes right after "Write Code" and "Git"?
A) Deploy  B) **Build & Test**  C) Monitor  D) Cloud

**Q3.** Cloud computing lets you use computing resources:
A) Only on-premise  B) **Over the internet**  C) Only via physical purchase  D) Only for storage

**Q4.** Which characteristic lets resources scale up/down with traffic?
A) On-demand access  B) **Scalability**  C) Accessibility  D) Managed infrastructure

**Q5.** Paying only for what you actually use is called:
A) Managed infrastructure  B) **Pay-as-you-go**  C) Scalability  D) On-demand access

**Q6.** Cloud resources being reachable from anywhere via the internet describes:
A) Scalability  B) **Accessibility**  C) Pay-as-you-go  D) Managed infrastructure

**Q7.** Which characteristic means the provider manages physical data centers and servers?
A) Scalability  B) Accessibility  C) **Managed infrastructure**  D) Pay-as-you-go

**Q8.** Which compute type requires you to manage OS + Application?
A) **VM**  B) Container  C) Serverless  D) None of these

**Q9.** Which compute type requires you to manage mainly just code?
A) VM  B) Container  C) **Serverless**  D) None of these

**Q10.** Public Cloud is:
A) Used by a single organization  B) **Owned by providers, shared among multiple customers**  C) A combination of public+private  D) Uses multiple providers

**Q11.** Private Cloud offers:
A) Shared infrastructure  B) **Dedicated infrastructure, high security**  C) Multiple vendors  D) Pay-per-use only

**Q12.** Hybrid Cloud combines:
A) Two public clouds  B) **Public and Private Cloud**  C) Multiple vendors only  D) None of these

**Q13.** Multi-Cloud primarily helps avoid:
A) Scalability issues  B) **Vendor lock-in**  C) Security risks only  D) Pay-as-you-go billing

**Q14.** Vendor lock-in means:
A) Easy migration between providers  B) **Dependency on one provider, making migration difficult**  C) Using multiple clouds  D) No cost implications

**Q15.** AWS provides services across which major categories?
A) Only compute  B) **Compute, Storage, Database, Network, Security**  C) Only storage and database  D) Only networking

---
## Day 30 — Amazon EC2 & Docker Containers

**Q1.** EC2 stands for:
A) **Elastic Compute Cloud**  B) Enterprise Cloud Compute  C) Elastic Container Cloud  D) Enterprise Container Compute

**Q2.** An EC2 instance is essentially:
A) A container  B) **A Virtual Machine**  C) A serverless function  D) A database

**Q3.** With a direct EC2 deployment, who manages OS updates and patches?
A) AWS entirely  B) **You (the user/team)**  C) No one  D) Only Docker

**Q4.** A container differs from a VM mainly because it:
A) Includes a full OS  B) **Shares the host OS kernel**  C) Is always larger  D) Cannot be portable

**Q5.** Which is a benefit of containers over VMs?
A) Slower startup  B) **Faster startup, lightweight**  C) Larger size  D) No portability

**Q6.** A Docker Image is best described as:
A) A running instance  B) **A template for a container**  C) A virtual machine  D) A cloud service

**Q7.** A Docker Container is:
A) A template  B) **A running instance of an image**  C) An AMI  D) A VPC

**Q8.** AMI stands for:
A) **Amazon Machine Image**  B) Amazon Managed Instance  C) Automated Machine Instance  D) Amazon Module Interface

**Q9.** Instance Type defines:
A) The firewall rules  B) **CPU, memory, storage, and network capacity**  C) The OS only  D) The VPC

**Q10.** A Security Group acts as:
A) A database  B) **A virtual firewall**  C) An AMI  D) A load balancer

**Q11.** Which port is used for SSH?
A) 80  B) 443  C) **22**  D) 8080

**Q12.** Which port is used for HTTPS?
A) 22  B) 80  C) **443**  D) 8080

**Q13.** What is the correct order of EC2 launch steps?
A) Security Group → AMI → Instance Type  B) **AMI → Instance Type → Security Group → Launch**  C) Launch → AMI → Instance Type  D) Instance Type → Launch → AMI

**Q14.** Docker Engine runs on:
A) Only local machines  B) **EC2 (and similar host machines)**  C) Only Windows  D) Only Kubernetes

**Q15.** With Docker on EC2, multiple containers can run:
A) Only one at a time  B) **On the same EC2 machine, simultaneously**  C) Only across separate EC2 instances  D) Never together

---
## Day 31 — ECS, EKS, Serverless & Key AWS Resources

**Q1.** ECS is described as:
A) **AWS-native container orchestration, simpler, no Kubernetes needed**  B) A Kubernetes-only service  C) A serverless function service  D) A database service

**Q2.** EKS is described as:
A) AWS-native only  B) **AWS-managed Kubernetes service**  C) A storage service  D) A networking service

**Q3.** Which is best suited for a team already using Kubernetes?
A) ECS  B) **EKS**  C) Lambda  D) EC2

**Q4.** In the ECS/EKS architecture, what routes traffic to decide which service handles a request?
A) Pod  B) **Ingress**  C) ECR  D) Node

**Q5.** The smallest deployable unit in Kubernetes is a:
A) Node  B) **Pod**  C) Cluster  D) Service

**Q6.** ECR is used to:
A) Run containers  B) **Store Docker images**  C) Load balance traffic  D) Manage IAM roles

**Q7.** AWS Lambda is an example of:
A) VM computing  B) Container computing  C) **Serverless computing**  D) None of these

**Q8.** With Lambda, you mainly manage:
A) The OS  B) The server  C) **Just your function code**  D) The VPC

**Q9.** With ECS/EKS, you mainly manage:
A) Just code  B) **Containers (AWS helps manage the infrastructure)**  C) Physical hardware  D) Nothing at all

**Q10.** Which AWS service is used for SQL databases?
A) DynamoDB  B) **RDS**  C) S3  D) EBS

**Q11.** Which AWS service is used for NoSQL databases?
A) RDS  B) **DynamoDB**  C) EBS  D) EFS

**Q12.** Which AWS service provides object storage?
A) EBS  B) EFS  C) **S3**  D) RDS

**Q13.** VPC stands for:
A) **Virtual Private Cloud**  B) Virtual Public Cloud  C) Verified Private Connection  D) Virtual Provider Cluster

**Q14.** A subnet is:
A) A separate VPC  B) **A smaller network inside a VPC**  C) A security group  D) A load balancer

**Q15.** Why use subnets?
A) To make everything public  B) **So not everything is accessible from the internet**  C) To increase cost  D) To disable networking

---
## Day 32 — Distributed Tracing & Swagger

**Q1.** Distributed tracing solves the problem of:
A) Slow databases  B) **Tracking a single request across multiple microservices**  C) Compiling code  D) Writing documentation

**Q2.** Spring Cloud Sleuth automatically adds ___ to every request.
A) Passwords  B) **Trace and Span IDs**  C) Timestamps only  D) SQL queries

**Q3.** A Trace represents:
A) A single service call  B) **The complete journey of one request**  C) A database index  D) A log file

**Q4.** A Span represents:
A) The entire request  B) **A single operation within a trace**  C) A database table  D) A Docker container

**Q5.** Which tool visualizes tracing data collected by Sleuth?
A) SonarQube  B) **Zipkin**  C) Jenkins  D) Swagger

**Q6.** Swagger is primarily used for:
A) CI/CD pipelines  B) **Generating interactive API documentation**  C) Container orchestration  D) Distributed tracing

**Q7.** Which annotation enables Swagger 2 in a Spring Boot app?
A) @EnableSwagger  B) **@EnableSwagger2**  C) @Swagger  D) @ApiDoc

**Q8.** Using `.any()` for both `RequestHandlerSelectors` and `PathSelectors` means:
A) No APIs are documented  B) **The entire API is documented**  C) Only POST APIs are documented  D) Documentation is disabled

**Q9.** Which type of bean configures Swagger's API selection?
A) Controller  B) **Docket**  C) Repository  D) Entity

**Q10.** Swagger UI is typically available at:
A) /api-docs  B) **/swagger-ui.html**  C) /actuator/swagger  D) /docs

---
## Day 33 — EKS + Node Group Creation Walkthrough

**Q1.** What is the first step in the EKS + Node Group setup?
A) Create Node Group  B) **Create a VPC**  C) Deploy Nginx  D) Open CloudShell

**Q2.** The EKS Cluster IAM Role's use case is set to:
A) EC2  B) **EKS Cluster**  C) Lambda  D) S3

**Q3.** Which policy is attached to the EKS Cluster IAM Role initially?
A) AmazonEKSWorkerNodePolicy  B) **AmazonEKSClusterPolicy**  C) AmazonS3FullAccess  D) AmazonRDSFullAccess

**Q4.** The Node IAM Role's trusted entity use case is:
A) EKS Cluster  B) **EC2**  C) Lambda  D) S3

**Q5.** Which policy is NOT attached to the Node IAM Role?
A) AmazonEKSWorkerNodePolicy  B) AmazonEKS_CNI_Policy  C) AmazonEC2ContainerRegistryReadOnly  D) **AmazonEKSClusterPolicy**

**Q6.** Which command connects `kubectl` to a newly created EKS cluster?
A) kubectl connect  B) **`aws eks update-kubeconfig --region <region> --name <cluster>`**  C) eks connect cluster  D) kubectl set-cluster

**Q7.** Which command verifies nodes are ready?
A) kubectl get pods  B) **kubectl get nodes**  C) kubectl get svc  D) kubectl get deployments

**Q8.** Which command deploys an Nginx container?
A) **`kubectl create deployment nginx --image=nginx`**  B) docker run nginx  C) kubectl run svc nginx  D) eks deploy nginx

**Q9.** Which command exposes the Nginx deployment externally?
A) kubectl expose pod nginx  B) **`kubectl expose deployment nginx --port=80 --type=LoadBalancer`**  C) kubectl create service nginx  D) docker expose nginx

**Q10.** Which command retrieves the public URL/external IP?
A) kubectl get nodes  B) **kubectl get svc**  C) kubectl get pods  D) kubectl describe cluster

---
## Day 34 — Git & GitLab Commands

**Q1.** Which command initializes a new Git repository?
A) git start  B) **git init**  C) git new  D) git create

**Q2.** Which command stages all changes, including deletions, repo-wide?
A) git add .  B) **git add -A**  C) git commit -a  D) git stage all

**Q3.** Which command creates AND switches to a new branch in one step?
A) git branch new  B) **`git checkout -b new`**  C) git switch new  D) git merge -b new

**Q4.** Merge differs from rebase because merge:
A) Rewrites history  B) **Preserves full history with a merge commit**  C) Deletes branches  D) Only works remotely

**Q5.** Which command safely force-pushes, checking for others' work first?
A) git push -f  B) **`git push --force-with-lease`**  C) git push --force-safe  D) git push -u

**Q6.** Which command discards unstaged changes to a file?
A) git reset  B) **`git restore <file>`**  C) git revert  D) git stash

**Q7.** Which `git reset` mode discards changes entirely?
A) --soft  B) --mixed  C) **--hard**  D) --keep

**Q8.** Which command creates a new commit that undoes a previous one, safe for shared history?
A) git reset  B) **git revert**  C) git restore  D) git stash

**Q9.** Which command temporarily shelves uncommitted changes?
A) git save  B) **git stash**  C) git hide  D) git pause

**Q10.** In GitLab, a Pull Request is called a:
A) Push Request  B) **Merge Request**  C) Commit Request  D) Branch Request

**Q11.** Where is a GitLab CI/CD pipeline defined?
A) Dockerfile  B) **`.gitlab-ci.yml`**  C) pom.xml  D) Jenkinsfile

**Q12.** In a GitLab pipeline, jobs within the same stage run:
A) Sequentially, always  B) **In parallel**  C) Never  D) Only on merge

**Q13.** The agent that executes GitLab CI/CD pipeline jobs is called a:
A) Executor  B) **Runner**  C) Worker  D) Agent

**Q14.** GitLab's protected branches prevent:
A) Cloning  B) **Direct pushes, requiring Merge Requests instead**  C) Pulling  D) Tagging

**Q15.** Which file lists patterns of files Git should NOT track?
A) .gitconfig  B) **.gitignore**  C) .gitattributes  D) .gitmodules

---
## Day 35 — Docker & SonarQube Commands

**Q1.** Which command lists all containers, including stopped ones?
A) docker ps  B) **`docker ps -a`**  C) docker images  D) docker list

**Q2.** Which command builds a Docker image from a Dockerfile?
A) docker create  B) **`docker build -t <name> .`**  C) docker run  D) docker compile

**Q3.** Which flag runs a container in detached (background) mode?
A) -it  B) **-d**  C) -p  D) -v

**Q4.** Which command opens an interactive shell inside a running container?
A) docker shell  B) **`docker exec -it <container> /bin/bash`**  C) docker attach  D) docker run -it

**Q5.** Which command removes all unused containers, networks, and dangling images?
A) docker clean  B) **docker system prune**  C) docker rm -all  D) docker reset

**Q6.** In Docker Compose, which command starts services in detached mode?
A) docker compose start  B) **`docker compose up -d`**  C) docker compose run  D) docker compose init

**Q7.** Where does SonarQube's Web UI run by default?
A) Port 8080  B) **Port 9000**  C) Port 3000  D) Port 443

**Q8.** Which tool runs static code analysis and sends results to a SonarQube server?
A) Docker  B) **SonarScanner**  C) Jenkins only  D) kubectl

**Q9.** For a Maven project, static analysis is typically run with:
A) mvn analyze  B) **`mvn sonar:sonar`**  C) mvn scan  D) mvn check

**Q10.** Where can SonarQube analysis properties be stored instead of CLI flags?
A) pom.xml only  B) **`sonar-project.properties`**  C) Dockerfile  D) .gitignore

**Q11.** The SonarQube Quality Gate status can be checked via:
A) docker ps  B) **the SonarQube Web API (`/api/qualitygates/project_status`)**  C) git log  D) kubectl get svc

**Q12.** In GitLab CI, SonarQube tokens are best stored as:
A) Hardcoded strings in `.gitlab-ci.yml`  B) **Masked CI/CD variables**  C) Plain text files  D) Commit messages

---
## Day 36 — CI/CD Concepts, Jenkins Setup & Pipeline Types

**Q1.** CI primarily focuses on:
A) Deploying to production  B) **Frequently merging and automatically building/testing code**  C) Only monitoring  D) Only packaging

**Q2.** The key difference between Continuous Delivery and Continuous Deployment is:
A) The build step  B) The test step  C) **The final production release step (manual vs automatic)**  D) The packaging tool used

**Q3.** Continuous Delivery requires:
A) Full automation with no human involvement  B) **A human to click "deploy" to production**  C) No testing at all  D) No packaging step

**Q4.** Which industries typically prefer Continuous Delivery over Deployment?
A) Fast-moving tech startups  B) **Regulated industries like banking/healthcare**  C) None — all use deployment  D) Only gaming companies

**Q5.** In the 5-stage CI/CD pipeline, which stage comes right after Build?
A) Deploy  B) **Test**  C) Package  D) Code

**Q6.** Where does the packaged Docker image typically get stored before deployment?
A) Directly on EC2  B) **A registry like Amazon ECR**  C) Local machine only  D) GitHub only

**Q7.** A Jenkinsfile is used to:
A) Configure Docker only  B) **Define a Jenkins pipeline as code**  C) Store SQL queries  D) Configure a VPC

**Q8.** In a Declarative Pipeline, which block defines WHERE the pipeline runs?
A) stages  B) **agent**  C) steps  D) post

**Q9.** Which block in a Declarative Pipeline runs actions after the pipeline finishes (success/failure)?
A) stages  B) steps  C) **post**  D) agent

**Q10.** A Scripted Pipeline is written inside which block?
A) `pipeline { }`  B) **`node { }`**  C) `stage { }`  D) `steps { }`

**Q11.** Scripted Pipelines support which constructs more easily than Declarative?
A) Stages only  B) **If-else, loops, try-catch**  C) Agents only  D) Post blocks only

**Q12.** Jenkins' one-time admin password (WAR install) is shown:
A) In a config file only  B) **In the console output during first startup**  C) Via email  D) It doesn't exist

**Q13.** In the MSI Windows installation, where is the initial admin password stored?
A) Console output only  B) **`C:\Program Files\Jenkins\secrets\initialAdminPassword`**  C) Desktop  D) Registry only

**Q14.** To run Jenkins on a custom port via the WAR file, you use:
A) `java -jar jenkins.war --port=9090`  B) **`java -jar jenkins.war --httpPort=9090`**  C) `jenkins --port 9090`  D) `docker run jenkins -p 9090`

---
## Day 37 — Jenkins + SonarQube Activities & Git Merge Conflicts

**Q1.** In the SonarQube token generation steps, which token type is selected for global analysis?
A) Project analysis  B) **Global Analysis**  C) User token  D) API token

**Q2.** In the Jenkins pipeline, which wrapper runs Maven commands with a specific Maven version?
A) withDocker  B) **withMaven**  C) withGit  D) withSonar

**Q3.** In the Scripted Pipeline example, what construct handles pipeline failure gracefully?
A) if-else only  B) **try-catch-finally**  C) switch-case  D) while loop

**Q4.** What does `currentBuild.result = 'FAILURE'` do?
A) Deletes the build  B) **Marks the current build as failed**  C) Restarts the pipeline  D) Skips the finally block

**Q5.** An "add/add" Git merge conflict occurs when:
A) One branch deletes a file  B) **Both branches independently create the same file with different content**  C) No files are changed  D) Only one branch has commits

**Q6.** After a merge conflict, which command tells you conflicts are fixed but a commit is still needed?
A) git log  B) **git status**  C) git diff  D) git branch

**Q7.** Resolving a conflict on `master` during a merge:
A) Automatically updates `develop` too  B) **Only affects `master` — `develop` keeps its own history**  C) Deletes `develop`  D) Merges automatically without editing

**Q8.** Which editor command is used in the walkthrough to manually resolve conflicts?
A) nano  B) **vi**  C) notepad  D) vim only, never vi

**Q9.** After fixing a merge conflict and staging the file, which command finishes the merge?
A) git merge --continue  B) **git commit**  C) git push  D) git stash pop

---
## Day 38 — Git Remote Workflows, Tags & Docker Activity

**Q1.** Before pushing a local repo to a remote for the first time, which command links them?
A) git push origin  B) **`git remote add origin <url>`**  C) git clone  D) git fetch

**Q2.** Which command both pushes AND sets upstream tracking for a branch?
A) `git push origin main`  B) **`git push -u origin main`**  C) git push --set-upstream only  D) git commit -u

**Q3.** To get an existing remote repository onto your local machine for the first time, you use:
A) git pull  B) **`git clone <url>`**  C) git fetch  D) git init

**Q4.** If a file is added directly on GitLab's web UI, which command brings it into your local clone?
A) git push  B) **`git pull origin main`**  C) git fetch only, nothing else  D) git merge

**Q5.** A Git Tag is primarily used to:
A) Delete old commits  B) **Mark an important commit/release in history**  C) Create a new branch  D) Resolve merge conflicts

**Q6.** In the Docker activity, which command builds the application JAR before creating a Docker image?
A) docker build  B) **`mvn clean install`**  C) docker run  D) git commit

**Q7.** Which command checks that the JAR file was actually created?
A) docker images  B) **`ls target`**  C) git status  D) docker ps

**Q8.** In the Dockerfile, which instruction copies the built JAR into the container?
A) ADD  B) **`COPY target/*.jar app.jar`**  C) RUN  D) FROM

**Q9.** Which instruction in the Dockerfile declares the port the app listens on?
A) PORT  B) **`EXPOSE 8081`**  C) OPEN 8081  D) LISTEN 8081

**Q10.** Which command actually starts the container after the image is built?
A) docker build  B) **`docker run -d --name myapp-container -p 8081:8081 myapp`**  C) docker start image  D) docker exec myapp

**Q11.** To remove a Docker image, you must first:
A) Do nothing extra  B) **Stop and remove any container using that image**  C) Restart Docker  D) Delete the Dockerfile

**Q12.** Which command removes a Docker image by name?
A) docker rm myapp  B) **`docker rmi myapp`**  C) docker delete myapp  D) docker clear myapp

---
*This is MCQ2 — covering Day 28 through Day 38. Combined with MCQ1 (Parts 1–4, Day 1–27), your prep now spans the full course to date.*
