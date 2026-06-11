name:           // name of the Workflow name
on:             // Defines when the workflow will run
jobs:           //
steps:          //

## Events of WorkFlow under 'on:'

| Event                   | When it Runs                           |
| ----------------------- | -------------------------------------- |
| `push`                | Code is pushed to a branch             |
| `pull_request`        | PR is opened, updated, reopened        |
| `workflow_dispatch`   | Manual trigger from GitHub UI          |
| `schedule`            | Runs on a cron schedule                |
| `workflow_run`        | Runs after another workflow completes  |
| `repository_dispatch` | Triggered by another repository or API |
| `release`             | Release is published                   |
| `create`              | Branch or tag created                  |
| `delete`              | Branch or tag deleted                  |
| `issues`              | Issue created/updated                  |
| `issue_comment`       | Comment added to issue                 |
| `pull_request_review` | Review submitted                       |
| `pull_request_target` | PR event with elevated permissions     |
| `fork`                | Repository forked                      |
| `watch`               | Repository starred                     |
| `deployment`          | Deployment created                     |
| `deployment_status`   | Deployment status changed              |
| `workflow_call`       | Called by another workflow             |

---

#### 1. push

on:
  push:
    branches:
      - develop

**Example:**
    Developer pushes code
      ↓
    Build
      ↓
    Run Unit Tests

#### 2. pull_request

on:
  pull_request:
    branches:
      - main

**Example:**
    Create PR to main
     ↓
    Run Playwright Tests
     ↓
    Allow Merge

#### 3. workflow_dispatch

on:
  workflow_dispatch:

**Example:**
    Click Run Workflow
        ↓
    Deploy QA Environment

#### 4. schedule

on:
  schedule:
    - cron: "0 2 * * *"     // "Minutes  Hours  Date  Month  Day"

**Example:**
    Every night
        ↓
    Run Regression Suite

#### 5. workflow_run

Workflow A:
name: Build

Workflow B:
on:
  workflow_run:
    workflows: ["Build"]

**Example:**
    Build Complete
        ↓
    Deploy Starts

#### 6. repository_dispatch

Repository A:
React App

Repository B:
Playwright Tests

**Example:**
    Deploy React App
        ↓
    Trigger Playwright Repo
        ↓
    Run Tests

This is exactly the scenario you asked about earlier.

#### 7. release

on:
  release:
    types:
      - published

**Example:**
    Release v2.0
        ↓
    Deploy Production

#### 8. create

on:
  create:

**Example:**
    feature/login branch created
        ↓
    Create QA Environment

#### 9. delete

on:
  delete:

**Example:**
    feature/login deleted
        ↓
    Destroy QA Environment

#### 10. issues

on:
  issues:

**Example:**
    New Bug Created
        ↓
    Send Teams Notification

#### 11. issue_comment

on:
  issue_comment:

**Example:**
    Comment:
    /retest
    ↓
    Run Tests Again

#### 12. pull_request_review

on:
  pull_request_review:

**Example:**
    Reviewer Approves PR
        ↓
    Start Deployment

#### 13. pull_request_target

on:
  pull_request_target:

**Example:**
    External Contributor PR
        ↓
    Run Safe Security Checks

Used mostly for open-source projects.

#### 14. fork

on:
  fork:

**Example:**
    Someone Forks Repository
        ↓
    Record Analytics

Rarely used.

#### 15. watch

on:
  watch:

**Example:**
    User Stars Repository
        ↓
    Send Notification

Rarely used.

#### 16. deployment

on:
  deployment:

**Example:**
    Deployment Created
        ↓
    Start Infrastructure Provisioning

#### 17. deployment_status

on:
  deployment_status:

**Example:**
    Deployment Successful
        ↓
    Notify Team

#### 18. workflow_call

Reusable Workflow:
on:
  workflow_call:

Main Workflow:
jobs:
  call-ci:
    uses: company/common-ci/.github/workflows/build.yml@main

**Example:**
    50 Repositories
        ↓
    Reuse Same Build Workflow
        ↓
    Maintain One CI Script
