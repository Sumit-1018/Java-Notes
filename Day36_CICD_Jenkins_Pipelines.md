# Day 36 - CI/CD Concepts, Jenkins Setup & Pipeline Types
*Thu, 20 Aug 2026*

## What Is CI/CD?

**CI/CD = Continuous Integration / Continuous Delivery (or Deployment)** — practices that **automate** moving code from a developer's machine to production. Runs automatically every time code is pushed.

- **CI** = Continuous Integration (one meaning)
- **CD** = Continuous Delivery **or** Continuous Deployment (two meanings — see below)

## 1. CI — Continuous Integration

- Developers frequently merge code into a shared repo (develop/master branch)
- Each merge automatically triggers:
  - **Build** — compile code (e.g. Maven build)
  - **Test** — run automated tests (JUnit/Surefire via `mvn test`)
  - **Feedback** — team notified immediately if the build/test fails

**Goal:** Catch bugs early, keep the main branch always working.

## 2. CD — Continuous Delivery vs Continuous Deployment

Both do the **same** steps: Build → Test → Package. The only difference is the **last** step (going live to PROD):

| | Continuous Delivery | Continuous Deployment |
|---|---|---|
| Final step | A **human** clicks to deploy to PROD | **Auto**-deploys to PROD, no human step |
| Summary | "Ready to ship, person gives final YES" | "Passes tests? It's live automatically" |

> Deployment = Delivery + auto-release (removes the manual click).

### Typical Pipeline

```
Code Commit -> Build -> Test -> Package (Docker) -> Staging -> Production
```

### Popular Tools

- GitLab CI/CD (built-in, uses `.gitlab-ci.yml` — see Day 34)
- Jenkins
- GitHub Actions
- AWS CodePipeline / CodeBuild

### Benefits

- Faster releases (automation, not manual)
- Fewer bugs (tests run on every change)
- Consistency (same process every time)
- Quick feedback (know instantly if something breaks)

---
## When to Use Delivery vs Deployment

### Use Continuous Delivery (manual click) when:
- Regulated industries: Banking, Finance, Healthcare (need approval/audit)
- Business timing matters (avoid sale/peak hours)
- Manager/QA/product sign-off needed
- Big or risky changes (DB migration, major feature)
- → **Most enterprises use this**

### Use Continuous Deployment (fully auto) when:
- Fast-moving tech firms (Netflix, Amazon, Google)
- Very strong automated testing (high trust, no manual QA gap)
- Small, frequent, low-risk changes (typo, bug fix, color tweak)
- Mature DevOps (monitoring, auto-rollback, feature flags)
- → **Speed over manual control**

> **Pizza analogy:** Delivery = a restaurant manager inspects the pizza before it leaves (control). Deployment = an auto pizza machine — made and shipped instantly (speed).

---
## Full Example — E-Commerce "Wishlist" Feature

Scenario: add a new Wishlist feature to a Spring Boot + ReactJS shopping app.

**Step 1 — Code & Commit (Developer)**
```bash
git add .
git commit -m "Add wishlist feature"
git push origin feature/wishlist
```

**Step 2 — Continuous Integration (AUTO)**
- Build: Maven builds the Spring Boot JAR
- Test: JUnit checks "Can user add item to wishlist?"
- Fail → pipeline stops, dev fixes. Pass → move on.

**Step 3 — Package (AUTO)**
```bash
docker build -t ecommerce-app:v2 .
docker push <registry>/ecommerce-app:v2
```
Pushed to **Amazon ECR** (Elastic Container Registry — the warehouse that stores Docker images).

**Step 4 — Deploy to Staging (AUTO)** — deploy to a PROD copy, run QA/automated tests.

**Step 5 — Deploy to Production**
- Delivery: release team clicks "Deploy" (safe window)
- Deployment: auto-deploys, no click
- AWS ECS/EKS pulls the image from ECR, runs it → Wishlist is LIVE

### Short Flow
```
Push -> [CI: Build+Test] -> Package(Docker->ECR) -> Staging+QA -> [CD: Deploy PROD] -> LIVE
```

---
## The CI/CD Pipeline — 5 Stages

1. **CODE** — Developer writes code and pushes to Git
2. **BUILD** — Code is compiled (e.g. Maven build)
3. **TEST** — Automated tests run (e.g. JUnit)
4. **PACKAGE** — App bundled into a Docker image, stored in ECR
5. **DEPLOY** — Image runs live on AWS ECS/EKS for customers

```
Code -> Build -> Test -> Package(Docker/ECR) -> Deploy(ECS/EKS) -> LIVE
```

> **Pizza analogy:** Order (code) → Prepare (build) → Taste-check (test) → Box (package) → Deliver (deploy) → Customer eats (live)

---
## Installing Jenkins

### Method 1 — WAR File

1. Download `jenkins.war` from https://get.jenkins.io/war-stable/jenkins.war
2. Save it in a local folder
3. Open a terminal, `cd` into that folder
4. Run: `java -jar jenkins.war` (custom port: `java -jar jenkins.war --httpPort=9090`)
5. Copy the one-time admin password shown in the console
6. Open `http://localhost:8080`
7. Paste the password on the "Unlock Jenkins" page
8. Click "Install suggested plugins"
9. Create the first Admin User (username, password, email)
10. Click "Start using Jenkins" — Dashboard is ready

### Method 2 — Windows MSI Installer (as a Service)

Best for a permanent setup (runs as a Windows service).

1. Download the Windows `.msi` installer from the Jenkins download page
2. Run the installer → Setup Wizard → Next
3. Choose destination folder → Next
4. Service logon: use a local/domain user (Test Credentials) → Next — *(`LocalSystem` = quick test only, not for production)*
5. Set port (default 8080) → Test Port → Next
6. Select the Java home directory → Next → Install
7. Finish — Jenkins runs as a Windows service
8. Open `http://localhost:8080`
9. Unlock using the password from: `C:\Program Files\Jenkins\secrets\initialAdminPassword`
10. Install suggested plugins → Create admin user → Done

---
## Declarative Pipeline

A structured, easy-to-read way to define a Jenkins CI/CD pipeline as code.

- The "Pipeline as Code" feature, written in a **Jenkinsfile**
- Uses a simple, fixed structure with clear blocks
- Preferred for most users — cleaner and requires less coding than Scripted Pipeline

### Where It's Written

1. In a file called `Jenkinsfile`, stored in your Git repository, **or**
2. Directly in the Jenkins UI: **Pipeline Job → Pipeline script**

### Key Building Blocks

| Block | Purpose |
|---|---|
| `pipeline { }` | Root block — everything goes inside this |
| `agent` | Defines WHERE the pipeline runs (e.g. `agent any`) |
| `stages { }` | Contains all the stages (Build, Test, Deploy, etc.) |
| `stage('name')` | One individual stage of the pipeline |
| `steps { }` | The actual commands/actions to execute |
| `post { }` | Actions that run AFTER the pipeline finishes, based on success/failure |

### Basic Structure

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building the app...'
                // Example: mvn clean package
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Example: mvn test
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to server...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully!'
        }
        failure {
            echo 'Pipeline failed - check logs.'
        }
    }
}
```

### Why Use Declarative Pipeline?

- Easy to read and maintain
- Jenkinsfile can be stored in Git
- Supports Pipeline as Code
- Less complex than Scripted Pipeline
- Built-in error/success handling via the `post` block
- Easy to understand and manage in CI/CD

---
## Scripted Pipeline

A flexible way to write Jenkins pipelines using **full Groovy code**.

- Written inside a `node { }` block
- Uses programming concepts: variables, if-else, loops, try-catch
- More flexible and powerful than Declarative Pipeline
- Best for complex, custom automation logic

`node` means the pipeline runs on a Jenkins agent — inside it, you write Groovy code and stages, controlling flow yourself.

### Basic Structure

```groovy
node {

    stage('Build') {
        echo 'Building the app...'
    }

    stage('Test') {
        echo 'Running tests...'
    }

    stage('Deploy') {
        echo 'Deploying to server...'
    }
}
```

### Example With Logic

```groovy
node {

    stage('Build') {
        echo 'Building...'
    }

    stage('Test') {
        def result = 'pass'

        if (result == 'pass') {
            echo 'Tests passed, moving on'
        } else {
            echo 'Tests failed'
        }
    }
}
```

### Declarative vs Scripted — Comparison

| Declarative | Scripted |
|---|---|
| Structured, simple syntax | Full Groovy programming |
| Easy to read | More flexible |
| Easier for beginners | More complex |
| Best for most CI/CD requirements | Useful for advanced/custom logic |
| Less coding required | Root: `node { }` |
| Root: `pipeline { }` | |

**Java analogy:**
```java
list.forEach(System.out::println)   // declarative style — "what to do"

for (Employee e : list) {
    System.out.println(e);          // scripted style — "how to do it, step by step"
}
```

### When to Use Scripted

- Complex if-else conditions
- Loops and dynamic steps
- Advanced custom workflows
- When Declarative Pipeline is too limited

---
## Activity 1 — Create a "Hello World" Pipeline

**Prerequisite:** Jenkins installed and running.

1. Open `http://localhost:8080`, log in to Jenkins
2. Left panel → **New Item** → Name: `HelloWorldPipeline` → select **Pipeline** → OK
3. Scroll to the Pipeline section, select the HelloWorld script from the dropdown:
   ```groovy
   pipeline {
       agent any

       stages {
           stage('Hello') {
               steps {
                   echo 'Hello World'
               }
           }
       }
   }
   ```
4. Click **Save**
5. Click **Build Now** (left panel) — Build #1 is created
6. Click **Build #1 → Console Output**

**Expected output:**
```
Hello World
Pipeline finished successfully.
```
