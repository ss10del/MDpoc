# UAT End-to-End Pipeline

This GitHub Actions workflow implements a comprehensive CI/CD pipeline for Salesforce UAT deployments.

## Overview

The pipeline includes the following stages:

- **Setup**: Evaluates scanner availability
- **Salesforce Validation**: Validates PR changes, runs tests, checks coverage, performs SCA
- **SCA/SAST Stage**: Runs npm audit with waivers
- **Automated Governance**: Hard gates for quality
- **CheckMarx SAST**: Security scanning
- **Fortify SAST/DAST**: Advanced security scanning
- **Approval & Merge Gate**: Handles PR approvals and merging
- **Deploy After Merge**: Deploys to UAT environment
- **Trigger CRT Tests**: Runs smoke tests via Copado Robotic Testing

## Configuration

Configure the following repository variables:

- `ORG_ALIAS`: Salesforce org alias (default: uat)
- `COVERAGE_THRESHOLD`: Minimum Apex coverage percentage (default: 85)
- `SOURCE_DIR`: Source directory path (default: force-app/main/default)
- `SFDX_AUTH_SECRET_NAME`: Secret name for auth URL (default: CRT_UAT_AUTHURL)
- `DELTA_FROM_COMMIT`: Commit SHA for delta calculations
- `FCLI_BOOTSTRAP_VERSION`: FCLI version
- `SCA_ENFORCEMENT_MODE`: SCA mode - enforce/warn/off (default: enforce)

## Secrets Required

- `CRT_UAT_AUTHURL`: Salesforce auth URL
- `CX_CLIENT_SECRET`: CheckMarx client secret
- `FOD_CLIENT_SECRET`: Fortify on Demand client secret
- `CRT_API_TOKEN`: Copado Robotic Testing API token
- `GH_PAT`: GitHub PAT for API calls

## Waiver Files

- `.github/sf-scanner-waivers.csv`: Waivers for Salesforce scanner violations
- `.github/sca-waivers.json`: Waivers for npm audit vulnerabilities