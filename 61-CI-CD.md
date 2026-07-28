# Stragegy:

    Out of the 2 models: 
        1) Git Flow
        2) Trunk Based Model
    We will go with "Trunk Based Model"

In trunk based development, we don't maintain multiple branches, rather we treat main branch with stable as a source of truth.

That means artifact will only be generated from the "main" branch. So, the steps in the workflow differ from main branch vs non-main branch.

Here is how we have to design our CI Pipeline / Workflows:
    If the commit happens on non-main branch:
        1) SAST Scan
        2) Testing ( Unit Testing & Integration Testing )
    If the commit happens to main branch:
        1) SAST Scan
        2) Testing ( Unit Testing & Integration Testing )
        3) Compile & Building the artifact
        4) Tag the artifact
        5) Publish the artifact to artifactory.

Then how do we deploy ?
    For deployment, we are going to maintain a separate workflow:

    Continuous Deployment vs Continuous Delivery

# Continuous Delivery vs Continuous Deployment

| Feature | Continuous Delivery | Continuous Deployment |
|---------|----------------------|-----------------------|
| **Definition** | Automatically builds, tests, and prepares every change for production, but requires **manual approval** before release. | Automatically builds, tests, and deploys every successful change directly to production without manual intervention. |
| **Production Deployment** | Manual approval required | Fully automatic |
| **Human Intervention** | Required before production deployment | None |
| **Automation Level** | Build, test, package, and deploy to staging are automated | Entire pipeline, including production deployment, is automated |
| **Release Trigger** | Manual approval or scheduled release | Successful completion of the pipeline |
| **Deployment Frequency** | As often as the business chooses | Every successful code change can be released |
| **Production Readiness** | Always production-ready | Always deployed to production |
| **Risk** | Lower due to manual verification | Higher if automated testing and monitoring are insufficient |
| **Rollback** | Usually manual | Often automated using deployment strategies (e.g., Blue/Green, Canary) |
| **Best Suited For** | Banking, healthcare, government, and other regulated industries | SaaS, cloud-native applications, and organizations with mature DevOps practices |

## Continuous Delivery

In Continuous Delivery, every code change is automatically:

1. Built
2. Tested
3. Packaged
4. Deployed to a staging or pre-production environment
5. Held for **manual approval** before production deployment

### Workflow

```text
Developer
    │
    ▼
Git Repository
    │
    ▼
Build
    │
    ▼
Automated Tests
    │
    ▼
Package Artifact
    │
    ▼
Deploy to Staging
    │
    ▼
Manual Approval
    │
    ▼
Production
```

### Example

A bank develops an online banking application.

- Developers merge code frequently.
- The CI/CD pipeline automatically builds and tests the application.
- The application is deployed to a staging environment.
- A release manager reviews and approves the release.
- After approval, the application is deployed to production.

---

## Continuous Deployment

Continuous Deployment extends Continuous Delivery by removing the manual approval step.

Every successful pipeline execution automatically:

1. Builds
2. Tests
3. Packages
4. Deploys to staging
5. Deploys directly to production

### Workflow

```text
Developer
    │
    ▼
Git Repository
    │
    ▼
Build
    │
    ▼
Automated Tests
    │
    ▼
Package Artifact
    │
    ▼
Deploy to Staging
    │
    ▼
Automatically Deploy to Production
```

### Example

A social media platform deploys a minor UI improvement.

- A developer merges the code.
- Automated tests and quality checks pass.
- The pipeline automatically deploys the change to production.
- Users receive the update within minutes, without requiring manual approval.

---

## Key Difference

The primary difference is **who decides when software is released to production**.

- **Continuous Delivery:** A person (such as a release manager or product owner) approves the production deployment.
- **Continuous Deployment:** The pipeline automatically deploys to production once all automated checks pass.

## Summary

| Aspect | Continuous Delivery | Continuous Deployment |
|--------|----------------------|-----------------------|
| Build Automation | ✅ | ✅ |
| Automated Testing | ✅ | ✅ |
| Artifact Creation | ✅ | ✅ |
| Staging Deployment | ✅ Automatic | ✅ Automatic |
| Production Deployment | Manual approval | Automatic |
| Manual Approval | Required | Not required |
| Production Release | On demand | Automatic after successful pipeline |
| Typical Users | Enterprises and regulated industries | SaaS companies and organizations with mature DevOps practices |

## Easy Way to Remember

- **Continuous Delivery** → **Always ready to release**
- **Continuous Deployment** → **Always releasing**






# CI/CD Pipeline Workflow

This repository uses two separate GitHub Actions workflows based on the branch where the commit is made.

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| `ci-nonmain.yaml` | Any **non-main** branch | Validate code quality before merging into `main` |
| `ci-main.yaml` | `main` branch | Build, package, version, publish, and deploy the application |

---

# Workflow 1: `ci-nonmain.yaml`

## Purpose

This workflow is executed for all feature, bugfix, release, or other non-main branches.

Its objective is to validate the code as early as possible without creating deployment artifacts or performing deployments.

## Activities

1. **Source Code Checkout**
   - Retrieves the latest source code from the repository.

2. **Static Application Security Testing (SAST)**
   - Performs static code analysis to identify security vulnerabilities and insecure coding practices.

3. **Unit Testing**
   - Executes unit tests to verify the correctness of individual functions, classes, or modules.

4. **Integration Testing**
   - Validates interactions between multiple components or services to ensure they work together correctly.

## Workflow

```text
Developer
    │
    ▼
Push Commit
(Non-Main Branch)
    │
    ▼
ci-nonmain.yaml
    │
    ▼
Checkout Source Code
    │
    ▼
SAST Scan
    │
    ▼
Unit Tests
    │
    ▼
Integration Tests
    │
    ▼
Pipeline Completed
```

## Outcome

- Ensures code quality and security.
- Detects defects before merging.
- Does **not** build artifacts.
- Does **not** perform deployments.

---

# Workflow 2: `ci-main.yaml`

## Purpose

This workflow is triggered whenever code is committed or merged into the `main` branch.

Its objective is to build, package, publish, and deploy the application across multiple environments.

## Activities

1. **Source Code Checkout**
   - Retrieves the latest source code.

2. **Static Application Security Testing (SAST)**
   - Detects security vulnerabilities before the build process.

3. **Unit Testing**
   - Validates individual software components.

4. **Integration Testing**
   - Verifies interactions between application modules and dependent services.

5. **Compile / Build**
   - Compiles the source code and produces deployable binaries or packages.

6. **Generate Artifact**
   - Creates the deployable artifact (e.g., JAR, WAR, Docker image, Helm chart).

7. **Versioning**
   - Assigns a unique version to the artifact based on the project's versioning strategy.

8. **Publish Artifact**
   - Pushes the versioned artifact to the artifact repository or container registry.

9. **Deploy to Development**
   - Deploys the published artifact to the Development environment.

10. **Deploy to QA**
    - Deploys the validated artifact to the QA environment.

11. **Deploy to Pre-Production**
    - Deploys the artifact to the Pre-Production environment for final validation.

12. **Deploy to Production**
    - Deploys the approved artifact to the Production environment.

## Workflow

```text
Developer
    │
    ▼
Merge / Commit to Main
    │
    ▼
ci-main.yaml
    │
    ▼
Checkout Source Code
    │
    ▼
SAST Scan
    │
    ▼
Unit Tests
    │
    ▼
Integration Tests
    │
    ▼
Compile / Build
    │
    ▼
Generate Artifact
    │
    ▼
Version Artifact
    │
    ▼
Publish Artifact
    │
    ▼
Deploy to DEV
    │
    ▼
Deploy to QA
    │
    ▼
Deploy to PRE-PROD
    │
    ▼
Deploy to PROD
```

## Outcome

- Produces a versioned, deployable artifact.
- Publishes the artifact to the artifact repository or container registry.
- Promotes the same artifact through Development, QA, Pre-Production, and Production environments.
- Ensures consistency by deploying the exact same version across all environments.

---

# Overall CI/CD Flow

```text
                     +-----------------------------+
                     |     Push to Non-Main        |
                     +-------------+---------------+
                                   │
                                   ▼
                           ci-nonmain.yaml
                                   │
                    +--------------+--------------+
                    │                             │
                    ▼                             ▼
               SAST Scan                   Unit Tests
                    │
                    ▼
             Integration Tests
                    │
                    ▼
               Validation Complete


                     +-----------------------------+
                     |      Merge to Main          |
                     +-------------+---------------+
                                   │
                                   ▼
                             ci-main.yaml
                                   │
                    +--------------+--------------+
                    │                             │
                    ▼                             ▼
               SAST Scan                   Unit Tests
                    │
                    ▼
             Integration Tests
                    │
                    ▼
              Compile / Build
                    │
                    ▼
             Generate Artifact
                    │
                    ▼
              Version Artifact
                    │
                    ▼
             Publish Artifact
                    │
                    ▼
                Deploy to DEV
                    │
                    ▼
                 Deploy to QA
                    │
                    ▼
             Deploy to PRE-PROD
                    │
                    ▼
              Deploy to PROD
```

# Summary

| Branch | Workflow | Activities | Artifact | Deployment |
|---------|----------|------------|----------|------------|
| Non-Main | `ci-nonmain.yaml` | Checkout → SAST → Unit Tests → Integration Tests | ❌ No | ❌ No |
| Main | `ci-main.yaml` | Checkout → SAST → Unit Tests → Integration Tests → Compile → Generate Artifact → Version → Publish → DEV → QA → PRE-PROD → PROD | ✅ Yes | ✅ Yes |