# Nano.GitHub.NuGet

> _Private Nuget registry setup and configuration._

***

## Table of Contents
* **[Summary](#summary)**
* **[Configuration](#configuration)**

## Summary
A private NuGet registry is a core requirement for maintaining a controlled, scalable, and efficient codebase.

Nano relies on a private NuGet server to distribute internal packages across services and libraries, ensuring consistent dependency management and secure access to proprietary 
components.

## Configuration
Private NuGet package hosting with GitHub Packages works out of the box when using GitHub Actions and the built-in `GITHUB_TOKEN`, which already provides the required authentication 
for publishing and consuming packages within your organization. For additional context on how GitHub Packages NuGet authentication works and the supported scenarios, see the 
**[official documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry)**.

> ⚠️ Be aware: consuming NuGet packages across repositories requires explicit access permissions. The package repository must grant access to the consuming workflow repository 
in order for restores to succeed within the organization.

For local development in Visual Studio, access to GitHub NuGet packages requires a Personal Access Token (PAT) with at least `read:packages` permissions. This token must be configured 
as the authentication method for the GitHub NuGet feed, allowing Visual Studio to authenticate and restore packages from private repositories within your organization.
