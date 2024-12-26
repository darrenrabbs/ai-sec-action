# AI Sec GitHub Action

A reusable GitHub Action to run the AI Sec linter for Terraform and Kubernetes configurations.

## About

The AI Sec GitHub Action provides a simple way to lint and scan your Terraform and Kubernetes infrastructure code using AI Sec. It bundles tools like `tfsec` and `tflint` for robust linting and security scanning.

## Usage

To use this action, include it in your GitHub workflows.

### Example Workflow

```yaml
name: Run AI Sec Linter

on:
  push:
    branches:
      - main
    paths:
      - "tests/terraform/**"
  pull_request:
    branches:
      - main
    paths:
      - "tests/terraform/**"

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Run AI Sec Linter
        uses: darrendev80/ai-sec-action@v1
        with:
          infra_dir: "./path/to/infra"
          openai_api_key: ${{ secrets.OPENAI_API_KEY }}
          upload_artifact: "true"
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
