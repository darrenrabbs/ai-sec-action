# AI Sec GitHub Action

A reusable GitHub Action to run the AI Sec linter for Terraform and Kubernetes configurations.

## About

The AI Sec GitHub Action provides a simple way to lint and scan your Terraform and Kubernetes infrastructure code using AI Sec. It bundles tools like `tfsec` and `tflint` for robust linting and security scanning.

## Usage

To use this action, include it in your GitHub workflows.

### Example Workflow

```yaml
name: "Run AI Sec"

on:
  workflow_dispatch: # Allows manual triggering of the workflow
  push:
    branches:
      - gitactions_test
    paths:
      - "tests/terraform/**"
  pull_request:
    branches:
      - gitactions_test
    paths:
      - "tests/terraform/**"

jobs:
  run-ai-sec:
    runs-on: ubuntu-latest

    steps:
      # Step 1: Checkout code
      - name: Checkout code
        uses: actions/checkout@v3

      # Step 3: Run AI Sec Linter
      - name: Run AI Sec Linter
        uses: ./.github/actions/ai_sec
        with:
          infra_dir: "${{ github.workspace }}/tests/terraform"
          config_path: "${{ github.workspace }}/config/config.yaml"
          fail_on_high: "true"
```

### Inputs

| Input            | Description                                   | Required | Example       |
| ---------------- | --------------------------------------------- | -------- | ------------- |
| `infra_dir`      | Path to the infrastructure directory to lint. | Yes      | `./infra`     |
| `openai_api_key` | OpenAI API key for AI Sec functionality.      | Yes      | `sk-12345...` |

### Outputs

None.

### Requirements

- **Docker**: The action uses a prebuilt Docker image to run the linter.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
