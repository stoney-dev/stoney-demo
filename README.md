# Stoney Demo

Welcome to the **Stoney Demo**! This project demonstrates "Requirements-as-Code" using Stoney, a framework designed to turn your technical requirements into automated, executable CI contracts.

## 🚀 Overview

Instead of scattered documentation, Stoney allows you to define your system requirements as YAML contracts. These contracts are executed automatically in your CI pipeline, validating your HTTP APIs, database connectivity, and runtime environment.

This repo showcases three core types of validation:

* **HTTP Checks:** Verify API endpoints, response payloads, and service health (`health_endpoint.yml`).
* **SQL Checks:** Ensure database connectivity and data invariants (`db_invariants.yml`).
* **Exec Checks:** Validate runtime dependencies (e.g., verifying Node.js is present) (`runtime_checks.yml`).



---

## 🛠 Features

* **Integrated CI/CD:** Runs directly in your GitHub Actions pipeline.
* **Job Summaries:** Automatically generates a visual, human-readable report in your GitHub Actions "Summary" tab.
* **Traceability:** Links every test to a `work_item` (e.g., `KAN-123`), keeping your tests accountable to your project management workflow.

---

## 💻 How to use this in your workflow

To integrate Stoney into your own project, add the following to your GitHub Actions workflow (`.github/workflows/stoney.yml`):

```yaml
jobs:
  stoney_checks:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Run Stoney Contracts
        uses: stoney-dev/stoney@v1
        with:
          base_url: "[https://your-api.com](https://your-api.com)"
          db_url: ${{ secrets.DATABASE_URL }}
          token: ${{ secrets.STONEY_TOKEN }}
          suite: "contracts/*.yml"
          require_work_item: "true"
          work_item_pattern: "^KAN-\\d+$"