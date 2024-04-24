# Terraform Validation
GitHub reusable workflow to run terraform validation

## Usage
To use this workflow, add a a new workflow file to your `.github/workflows` directory containing the following:

```yaml
name: Validate terraform
on:
  pull_request:
    paths:
      - ".infra/terraform/**"

jobs:
  validate-terraform:
    strategy:
      matrix:
        path: [".infra/terraform/ci", ".infra/terraform/service"]
    uses: attest/terraform-validation/.github/workflows/check-terraform.yaml@main
    with:
      path: ${{ matrix.path }}
    secrets:
      AWS_ACCESS_KEY: ${{ secrets.AWS_ACCESS_KEY }}
      AWS_SECRET_KEY: ${{ secrets.AWS_SECRET_KEY }}
      GITHUB_USERNAME: "attest-admin"
      PAT_ATTEST_ADMIN_CI: ${{ secrets.PAT_ATTEST_ADMIN_CI }}
```

Take note of the `paths` variable in the `on` definition that defines what files need to change in order for this workflow to run. Also take note of the `matrix.path` variable that is set, this is what defines where your terraform definitions are that need to be checked.
