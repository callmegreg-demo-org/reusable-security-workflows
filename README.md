# Overview
This repo is intended to inspire the use of [reusable workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) to centralize security testing configuration.

# Current capabilities
- SAST with GitHub's [CodeQL](https://codeql.github.com/)
- Dependency analysis with GitHub's [Dependency Review](https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/about-dependency-review)
- IaC analysis with AquaSecurity's [TFSec](https://github.com/aquasecurity/tfsec)
- Container image analysis with Anchore's [grype](https://github.com/anchore/scan-action)

# Example workflows
## [strict-security-scan.yml](https://github.com/callmegreg-demo-org/my-reusable-workflows/blob/main/.github/workflows/strict-security-scan.yml)
This workflow is designed to demonstrate centralized control. It automatically detects relevant tests and enforces applicable scans & severity gates, all the while minimizing the complexity for downstream caller repos.
