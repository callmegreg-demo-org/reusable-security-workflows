# Overview
This repo is intended to inspire the use of [reusable workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) to centralize security testing configuration.

# Pre-requisites
- Some of the jobs in the example workflows require [GitHub Advanced Security](https://docs.github.com/en/get-started/learning-about-github/about-github-advanced-security) to be enabled for private/internal repos.

# Current capabilities
- SAST with GitHub's [CodeQL](https://codeql.github.com/)
- Dependency analysis with GitHub's [Dependency Review](https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/about-dependency-review)
- IaC analysis with AquaSecurity's [TFSec](https://github.com/aquasecurity/tfsec)
- Container image analysis with Anchore's [grype](https://github.com/anchore/scan-action)

# Example workflows
## Continuous Integration - Strict
Workflow file: [strict-security-scan.yml](https://github.com/callmegreg-demo-org/my-reusable-workflows/blob/main/.github/workflows/strict-security-scan.yml)

This workflow demonstrates centralized control. It automatically detects relevant testing capabilities, fails the job based on the severity of alerts, and minimizes the customizations & complexity for downstream caller repos.

_Notable features:_
- Only run applicable jobs
- Applicable CodeQL languages are automatically detected and set
- Each job is configured to fail on any `medium` severity or higher alerts
- The caller workflow can specify their java version

## Continuous Integration - Flexible
Workflow file: [flexible-security-scan.yml](https://github.com/callmegreg-demo-org/my-reusable-workflows/blob/main/.github/workflows/flexible-security-scan.yml)

This workflows demonstrates developer control. It gives more flexibility to the caller repo about what the workflow does.

_Notable features:_
- Ability to opt out of any of the testing capabilities
- Ability to specify which languages should be scanned by CodeQL
- No alert/severity based status check failures

## Caller Workflow
Workflow file: [regression-testing.yml](https://github.com/callmegreg-demo-org/my-reusable-workflows/blob/main/.github/workflows/regression-testing.yml)

This is an example caller workflow that would be implemented by the downstream repositories that call your centralized workflow.

`secrets:inherit` is only required if you would like to access **_caller_** repository secrets or organization secrets in the workflow run. It will **_not_** allow the caller workflow to access **_centralized_** repository secrets.
