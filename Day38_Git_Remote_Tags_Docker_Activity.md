# Day 38 - Git Remote Workflows, Tags & Docker Image Activity
*Mon, 24 Aug 2026 (Week 9)*

## Activity 4 — Pushing a Local Repository to a Remote Repository

1. Select your local repository in the terminal:
   ```bash
   cd my-app
   ```
2. Switch to the `master` branch
3. Copy the HTTPS URL from your GitLab project
4. Back in the terminal:
   ```bash
   git remote add origin <https url of GitLab project>
   git add .
   git commit -m "initial commit"
   git push -u origin main
   ```
   - **username:** your GitLab account username
   - **password:** password/access token generated with the GitLab project
   - Data gets added to your GitLab account
5. Go to the GitLab project and verify the files were added

## Activity 5 — Creating a Remote Repository & Cloning It Locally

1. Log in to your GitLab account
2. Create a new project, e.g. `Git_clone_project`
3. Copy the HTTPS URL of the GitLab project
4. In the terminal:
   ```bash
   git clone <https url of Gitlab project>
   ```
   The remote repository is cloned locally.
5. Change into the cloned directory:
   ```bash
   cd Git_clone_repository
   ```
6. Create a new file:
   ```bash
   touch file1
   echo "File 1 added to clone_repository" > file1
   git add file1
   git commit -m "file1 added to git_clone_project"
   git status
   ```
7. Push it:
   ```bash
   git push origin main
   # username
   # password
   ```
   `file1` is pushed to the remote repo.

## Activity 6 — Pulling Remote Changes Into a Local Repository

1. Log in to GitLab, open `Git_Clone_Project` (already has `file1`)
2. In GitLab directly: click **+**, create a new file (e.g. `file2`), add content, commit to the `main` branch
3. In the terminal, `cd` into `git_clone_project` — at this point it still only shows `file1` locally
4. Pull the new file down:
   ```bash
   git pull origin main
   ```
5. Run `dir`/`ls` again — now both `file1` and `file2` exist locally

---
## Git Tag

Marks an important commit in the application's development history — a label given to an important version/release.

### Example — First Release

```
One App

Commit1 → Commit2 → Commit3
                       |
                   Final v1.0
                     (Tag)
```

### Example — Next Release, After Adding a Feature

```
                                  New Feature
                                     |
Commit1 → Commit2 → Commit3 → Commit4 → Commit5 → Commit6
             |                                       |
         Final v1.0                              Final v2.0
           (Tag)                                    (Tag)
```

Each tag marks a specific, meaningful commit (like a shipped release) so it can be referenced or checked out later without hunting through the full commit log. *(See Day 34 for the actual `git tag` commands: `git tag`, `git tag -a v1.0.0 -m "..."`, `git push origin --tags`.)*

---
## Docker Activity — Building & Running a Spring Boot Image From Scratch

### Step 1 — Check Docker Version

```bash
docker --version
```

### Step 2 — Check Running Containers

```bash
docker ps      # lists only currently RUNNING containers
```

### Step 3 — Navigate to the Project

```bash
cd map-employee-crud-sonar-issues/
dir            # check directory contents
```

### Step 4 — Build the Application JAR

```bash
mvn clean install
ls target      # confirm the JAR file was created
```

### Step 5 — Create a Dockerfile

In the project root folder:
```bash
vi Dockerfile
```
Press `i` to enter insert mode, paste the content below, then `Esc` followed by `:wq` to save and quit.

```dockerfile
# Step 1: Use an official base image (OpenJDK 17)

# for x86_64 architecture
# FROM openjdk:17-jdk-alpine

# for ARM64 architecture
FROM eclipse-temurin:17-jdk

# Step 2: Set the working directory inside the container
WORKDIR /app

# Step 3: Copy your JAR file into the container
COPY target/*.jar app.jar

# Step 4: Expose the port your app runs on
EXPOSE 8081

# Step 5: Run the application
CMD ["java", "-jar", "app.jar"]
```

> Note the architecture-specific base image comment — `openjdk:17-jdk-alpine` for x86_64 machines, `eclipse-temurin:17-jdk` for ARM64 (e.g. Apple Silicon Macs). Using the wrong one can cause the container to fail or run very slowly under emulation.

### Step 6 — Build the Docker Image

```bash
docker build -t myapp .
docker images     # confirm "myapp" is now listed
```

### Step 7 — Create and Run the Container

```bash
docker run -d --name myapp-container -p 8081:8081 myapp
```

### Step 8 — Verify the Container Is Running

```bash
docker ps
```

### Step 9 — Access the Application

```
http://localhost:8081/api/employees
```

### Step 10 — Stop the Container

```bash
docker stop myapp-container
```

### Cleanup — Removing the Image and Container

```bash
# remove the image (by name or ID)
docker rmi myapp

# remove the container — stop it first, then remove
docker stop myapp-container
docker rm myapp-container
```

> This mirrors the general Docker command reference from Day 35 — this activity is that reference applied to a real Spring Boot project end to end: build the JAR → write the Dockerfile → build the image → run, verify, and tear down the container.
