# GitHub Actions Workflow Documentation

## Overview

This document provides a detailed explanation of the GitHub Actions workflow defined in the YAML file named `github-cicd-pipeline.yml`. The workflow automates a Continuous Integration/Continuous Deployment (CI/CD) pipeline for a web application hosted on GitHub. The workflow is triggered on pull requests to the `master` branch.

## Workflow Structure

The workflow is organized into multiple jobs, each responsible for specific tasks in the CI/CD process.

### 1. **build-test Job**

- **Purpose:** Executes on pull requests to the `master` branch and performs initial build and test operations.

- **Steps:**
  - Echoes a message indicating that the application is being built and tested.

### 2. **docker-build-push Job**

- **Purpose:** Depends on the completion of the `build-test` job. It builds a Docker image for the web application, pushes it to DockerHub, and tags it with the commit SHA.

- **Steps:**
  - Checks out the source code using `actions/checkout`.
  - Sets up Docker Buildx for multi-platform builds.
  - Logs in to DockerHub using the provided DockerHub credentials.
  - Builds and pushes the Docker image using `docker/build-push-action`, tagging it with both `latest` and the GitHub commit SHA.

### 3. **update-deployment Job**

- **Purpose:** Depends on the completion of the `docker-build-push` job. Updates the deployment YAML file with the latest Docker image tag.

- **Steps:**
  - Retrieves the Docker image tag from the output of the previous job.
  - Checks out the code and pulls the latest changes from the pull request branch.
  - Sets file permissions for the deployment YAML file.
  - Updates the deployment YAML file with the new Docker image tag using `sed`.
  - Commits the changes with a commit message indicating the image tag update.
  - Pushes the changes back to the pull request branch.

### 4. **add_labels Job**

- **Purpose:** Depends on the completion of the `update-deployment` job. Adds the "preview" label to the associated pull request.

- **Steps:**
  - Checks out the repository using `actions/checkout`.
  - Adds the "preview" label to the pull request using `actions-ecosystem/action-add-labels`.

## Conclusion

This GitHub Actions workflow automates the entire CI/CD pipeline, including building and testing the application, Dockerizing the application, updating the deployment configuration, and adding a label to indicate that the changes are ready for preview. It is designed to enhance the development workflow by providing automated testing and deployment processes.

For more details about each job and the specific actions used, refer to the respective documentation of the GitHub Actions used in this workflow.
