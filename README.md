

# Build and Deploy Configuration

## Buildspec.yaml

The `buildspec.yaml` file defines the build, pre-build, build, and post-build phases for the CI/CD pipeline. It includes commands for various tasks such as installing dependencies, building Docker images, running tests, and pushing artifacts.

### Phases

#### Install Phase

- Fetches variables from AWS Secret Manager.
- Installs required tools like Helm and AWS CLI.
- Retrieves necessary secrets from AWS Secrets Manager.
- Sets up environment variables.

#### Pre-Build Phase

- Lints Dockerfiles and checks for errors.
- Builds Docker images for testing.
- Checks test coverage.
- Prepares Helm chart values for deployment.

#### Build Phase

- Creates container images based on the environment.
- Tag the container images.
- Pushes container images to the Amazon ECR repository.

#### Post-Build Phase

- Handles post-build operations like tagging releases.
- Cleans up temporary files.

### Artifacts

The artifacts section specifies the files generated during the build process that will be passed to the next stage in the pipeline.

## Deployspec.yaml

The `deployspec.yaml` file defines the deployment process after the build is successful. It includes commands for deploying Kubernetes resources using Helm charts.

### Phases

#### Install Phase

- Fetches necessary secrets and tools required for deployment.
- Sets up Kubernetes configuration.

#### Post-Build Phase

- Assumes role for accessing the Kubernetes cluster.
- Updates the Kubernetes configuration.
- Upgrades the Helm chart for deployment.
- Notifies about deployment status via Slack.
- Cleans up temporary files.

### Artifacts

The artifacts section specifies the output of the deployment process, which includes a JSON file containing information about the deployed image.

