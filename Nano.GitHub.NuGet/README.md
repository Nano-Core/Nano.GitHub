# Nano.GitHub.NuGet

> _Private Nuget registry setup and configuration._

***

## Table of Contents
* **[Summary](#summary)**
* **[Configuration](#configuration)**

## Summary
A private NuGet registry is a core requirement for maintaining a controlled, scalable, and efficient codebase.

Nano relies on a private NuGet server to distribute internal packages across services and libraries, ensuring consistent dependency management and secure access to 
proprietary components.

## Configuration
To configure private NuGet package hosting using GitHub Packages, follow the **[official documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry)**.  

Nano requires the following environment variables to be defined for applications publishing NuGet packages.  

| Variable         | Value                                                    | Description                                      |
| ---------------- | -------------------------------------------------------- |------------------------------------------------- |
| `NUGET_HOST`     | `https://nuget.pkg.github.com/{{org-name}}/index.json`   | URL to the GitHub NuGet package registry         |
| `NUGET_APIKEY`   | `ghp_xxxxxxxxxxxxxxxxxxxx`                               | GitHub Personal Access Token (PAT)               |
| `NUGET_USERNAME` | `your-github-username`                                   | GitHub username associated with the PAT          |

All variables must be configured as GitHub repository or organization secrets.  
