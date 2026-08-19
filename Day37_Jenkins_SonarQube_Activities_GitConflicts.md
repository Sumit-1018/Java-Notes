# Day 37 - Jenkins + SonarQube Pipeline & Git Merge Conflicts
*Fri, 21 Aug 2026*

## Activity 2 — Declarative Pipeline With SonarQube (via Docker)

### Run SonarQube in Docker

```bash
docker run --rm -d -p 9000:9000 -v sonarqube_extensions:/opt/sonarqube/extensions sonarqube
```
Then open `http://<External IP>:9000/` in a browser.

### Generate a SonarQube Token

1. Click **My Account**
2. Go to **Security**
3. Give the token a name
4. Select token type: **Global Analysis**
5. Generate the token

```
Example token: sqa_bbfdf90d8014b1e4f7cb33c9fa73ba3a4ceddf1f
```

### Declarative Pipeline Script

Enter this in the Jenkins Pipeline Script box, swapping in your own generated SonarQube token:

```groovy
pipeline {

    agent any

    stages {

        stage('checkout source code') {
            steps {
                git branch: 'main',
                    url: 'https://gitlab.com/deepakgcp25/easyfly.git'
            }
        }

        stage('build') {
            steps {
                withMaven(maven: 'maven3.9.9') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('static code analysis') {
            steps {
                withMaven(maven: 'maven3.9.9') {
                    sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqa_d6b604c1fb6b0cfd71a435332b136c18787d74db'
                }
            }
        }

        stage('test') {
            steps {
                withMaven(maven: 'maven3.9.9') {
                    sh 'mvn test'
                }
            }
        }

        stage('public url') {
            steps {
                echo 'Application URL: http://localhost:8081'
            }
        }

        stage('Run Application') {
            steps {
                withMaven(maven: 'maven3.9.9') {
                    sh 'mvn spring-boot:run -Dspring-boot.run.profiles=dev'
                }
            }
        }
    }
}
```

**Next step:** Save and build the pipeline, then observe the app on port **8081**.

---
## Activity 3 — Same Pipeline, Scripted Syntax

Same steps as Activity 2, but written as a **Scripted Pipeline** (`node { }` instead of `pipeline { }`), with `try/catch/finally` for error handling.

```groovy
node {

    try {

        // Checkout the code from the Git repository
        stage('Checkout Code') {
            echo 'Checking out the repository...'
            git branch: 'main',
                url: 'https://gitlab.com/deepakgcp25/easyfly.git'
        }

        // Build the project using Maven
        stage('Build') {
            echo 'Building the project using Maven...'
            withMaven(
                globalMavenSettingsConfig: '',
                jdk: 'JDK17',
                maven: 'maven3.9.9',
                mavenSettingsConfig: '',
                traceability: true
            ) {
                sh 'mvn clean package'
            }
        }

        stage('Static Code Analysis') {
            withMaven(
                globalMavenSettingsConfig: '',
                jdk: 'JDK17',
                maven: 'maven3.9.9',
                mavenSettingsConfig: '',
                traceability: true
            ) {
                sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqa_f797304309c46b6f64374598cb9d6e4c969742f4'
            }
        }

        stage('Unit Testing') {
            withMaven(
                globalMavenSettingsConfig: '',
                jdk: 'JDK17',
                maven: 'maven3.9.9',
                mavenSettingsConfig: '',
                traceability: true
            ) {
                sh 'mvn test'
            }
        }

        stage('Publish_URL') {
            echo 'Application running on: http://localhost:8081'
        }

        stage('Run Application') {
            withMaven(
                globalMavenSettingsConfig: '',
                jdk: 'JDK17',
                maven: 'maven3.9.9',
                mavenSettingsConfig: '',
                traceability: true
            ) {
                sh 'mvn clean install spring-boot:run'
            }
        }

    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e

    } finally {
        echo 'Cleaning up after pipeline execution...'
    }
}
```

> Notice the `try/catch/finally` wrapping the whole pipeline — this is exactly the kind of custom control-flow logic that a Declarative Pipeline can't express directly (see Day 36's "When to Use Scripted" section), and is one of Scripted Pipeline's key advantages.

---
## Git Merge Conflicts — Hands-On Walkthrough

A worked example showing how an **add/add conflict** happens and gets resolved, across two rounds (`file2`, then `file3`).

### Round 1 — Conflict in `file2`

```bash
touch file2
echo "file2 added in master" > file2
git add file2
git commit -m "file2 added in master"
# [master 53662a1] file2 added in master

git checkout develop
touch file2
echo "file2 added in develop" > file2
git add file2
git commit -m "file2 in develop"
# [develop 275f85a] file2 in develop

git checkout master
git branch
#   develop
# * master

git merge develop
# Auto-merging file2
# CONFLICT (add/add): Merge conflict in file2
# Automatic merge failed; fix conflicts and then commit the result.
```

Both branches independently created `file2` with different content — Git can't automatically decide which version "wins," so it flags an **add/add conflict**.

### Resolving the Conflict

```bash
vi file2
# manually edit the file to keep both/resolved content:
#   file2 added in master
#   file2 added in develop

git add file2
git commit -m "conflict is resolved"
# [master 27f9c19] conflict is resolved
```

After committing the resolution, switching back to `develop` still shows develop's **original, unmerged** version — the conflict resolution only affected `master`:
```bash
git checkout develop
cat file2
# file2 added in develop
```

### Round 2 — Same Conflict Pattern With `file3`

```bash
git checkout master
touch file3
echo "file3 added in master" > file3
git add file3
git commit -m "file3 in master"

git checkout develop
touch file3
echo "file3 is added in develop" > file3
git add file3
git commit -m "file3 in develop"

git checkout master
git merge develop
# Auto-merging file3
# CONFLICT (add/add): Merge conflict in file3
```

```bash
vi file3
# resolve — kept master's version this time:
#   file3 added in master

git add file3
git status
# On branch master
# All conflicts fixed but you are still merging.
#   (use "git commit" to conclude merge)
#
# Changes to be committed:
#     modified:   file3

git commit -m "conflict resolved"
```

### Key Takeaways

- An **add/add conflict** happens when both branches create the same file independently with different content
- `git status` during a conflict clearly tells you: conflicts are fixed, but you still need to `git commit` to conclude the merge
- Resolving a conflict on one branch (e.g. `master`) does **not** change the other branch (`develop`) — each branch keeps its own history until merged again
