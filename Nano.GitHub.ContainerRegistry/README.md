# Nano.GitHub.ContainerRegistry

> _Private container registry setup and configuration._

***

## Table of Contents
* **[Summary](#summary)**
* **[Configuration](#configuration)**

## Summary
Nano requires a container registry to publish container images for applications and services. This enables consistent distribution and deployment of containerized 
workloads across environments.  

## Configuration
To configure a private container registry using GitHub, follow the **[official documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)**.  
  
Nano requires the following environment variables for deploying application and infrastructure containers.  

| Variable                          | Value                                              | Description                                            |
| --------------------------------- |--------------------------------------------------- | ------------------------------------------------------ |
| `CONTAINER_REGISTRY_HOST`         | `ghcr.io/{{org-name}}`                             | GitHub Container Registry host (must be lowercase).    |
| `CONTAINER_REGISTRY_USERNAME`     | `your-github-username`                             | GitHub username associated with the PAT.               |
| `CONTAINER_REGISTRY_PASSWORD`     | `ghp_xxxxxxxxxxxxxxxxxxxx`                         | GitHub Personal Access Token (PAT).                    |
| `CONTAINER_REGISTRY_SOURCE_LABEL` | `https://github.com/{{org-name}}/{{image-name}}`   | Source repository reference for the container image.   |

> ⚠️ These values are also required during Kubernetes deployment. Ensure they are recorded securely and made available to deployment pipelines.

It is also possible to use GitHub Actions built-in authentication:

| Option      | Value                           |
| ----------- | ------------------------------- |
| Username    | `${{ github.actor }}`           |
| Password    | `${{ secrets.GITHUB_TOKEN }}`   |

> ⚠️ When using this approach, the repository must be explicitly linked to the container package on GitHub using `CONTAINER_REGISTRY_SOURCE_LABEL` for proper access control.
