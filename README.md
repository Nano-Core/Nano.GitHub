# Nano.GitHub

> _Required GitHub components for Nano._

***

## Table of Contents
* **[Summary](#summary)**
* **[Nano.GitHub.NuGet](https://github.com/Nano-Core/Nano.GitHub/tree/master/GitHub.NuGet)**
* **[Nano.GitHub.ContainerRegistry](https://github.com/Nano-Core/Nano.GitHub/tree/master/GitHub.ContainerRegistry)**

## Summary
Establishing a reliable and scalable .NET development workflow on Kubernetes requires a well-configured GitHub foundation.

Nano depends on GitHub as a central platform for source control, package distribution, container management, and releases. Proper configuration ensures secure, consistent, 
and automated delivery across services.

In addition to repository setup, several supporting services and tools are required to enable the full Nano ecosystem.

After creating a GitHub account and organization, review the organization settings carefully. Pay particular attention to:

| Area                     | Recommendation                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| Branch Protection        | Enforce pull request reviews, status checks, and restrict direct pushes         |
| Security Configuration   | Enable dependency scanning, secret scanning, and code scanning                  |
| Access Control           | Apply least-privilege access and manage team permissions                        |
| Repository Policies      | Standardize settings across repositories where possible                         |

These configurations form the baseline for a secure and maintainable development environment.
