# AWS Service Control Policies

[![Validate SCPs](https://github.com/hammadhaqqani/aws-service-control-policies/actions/workflows/validate.yml/badge.svg)](https://github.com/hammadhaqqani/aws-service-control-policies/actions/workflows/validate.yml)
[![GitHub Pages](https://github.com/hammadhaqqani/aws-service-control-policies/actions/workflows/pages.yml/badge.svg)](https://hammadhaqqani.github.io/aws-service-control-policies/)
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-ffdd00?style=flat&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/hammadhaqqani)

A collection of AWS Organizational Service Control Policies (SCPs) and deployment scripts for enforcing security guardrails across your AWS Organization.

## What Are Service Control Policies?

[Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) (SCPs) are IAM-like policies applied by a parent AWS Account to child accounts via [AWS Organizations](https://aws.amazon.com/organizations/). They can whitelist or blacklist AWS services so that not even the Root Account or a full IAM Administrator can call the specified API actions.

> **Note:** No matter what SCPs are attached, the root user can always: change root password, manage root access keys, enable/disable MFA, and manage x.509 keys.

## Policies

### Security Controls

The base Security Controls SCP enforces the following across all accounts:

- **Deny CloudTrail Tampering** — Prevents deletion, update, or stopping of CloudTrail
- **Deny Billing Modifications** — Prevents modification of account contacts and settings
- **Deny Leaving Organization** — Prevents accounts from leaving the AWS Organization

### Additional Policies to Consider

- Disable consumer features (Alexa for Business, WorkMail, etc.)
- Restrict usage of specific AWS regions
- Disable use of AWS Managed IAM Policies

## Project Structure

```
.
├── Policies/                       # SCP JSON policy documents
├── enable_scp.sh                   # Enable SCP usage in your Organization
├── deploy_scp.sh                   # Deploy all SCPs from Policies directory
├── apply_scp.sh                    # Attach Security Controls SCP to all accounts
└── .github/workflows/
    ├── validate.yml                # CI: JSON syntax validation
    └── pages.yml                   # GitHub Pages deployment
```

## Quick Start

```bash
# Clone the repo
git clone https://github.com/hammadhaqqani/aws-service-control-policies.git
cd aws-service-control-policies

# 1. Enable SCPs in your Organization
./enable_scp.sh

# 2. Deploy all policies
./deploy_scp.sh

# 3. Attach Security Controls to all accounts
./apply_scp.sh
```

> If you get `PolicyTypeNotEnabledException`, you need to run `enable_scp.sh` first.

## Prerequisites

- AWS CLI configured with Organization admin credentials
- `jq` for JSON processing
- Access to AWS Organizations master account

## CI/CD

Every push triggers automated JSON validation via GitHub Actions, ensuring all SCP policy documents are syntactically valid.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](LICENSE)

## Author

**Hammad Haqqani** — DevOps Architect & Cloud Engineer

- Website: [hammadhaqqani.com](https://hammadhaqqani.com)
- LinkedIn: [linkedin.com/in/haqqani](https://www.linkedin.com/in/haqqani)
- Email: phaqqani@gmail.com

---

## Support

If you find this useful, consider buying me a coffee!

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/hammadhaqqani)
