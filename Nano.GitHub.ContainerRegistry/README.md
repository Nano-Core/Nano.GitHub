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
Private container image hosting with GitHub Container Registry (GHCR) works out of the box when using GitHub Actions and the built-in `GITHUB_TOKEN`, which provides the required 
authentication for both publishing and consuming images within your organization. For additional details on authentication flows and supported scenarios, see the 
**[official documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)**.

For local development, access to GitHub Container Registry requires authentication using a Personal Access Token (PAT) with at least `read:packages` permissions. This token must be 
used to log in to the registry (e.g. via `docker login`), enabling Docker to pull private images from repositories within your organization.

> ⚠️ The repository must be linked to the container package via `CONTAINER_REGISTRY_SOURCE_LABEL` to ensure proper access control. This is preconfigured for all Nano applications.
