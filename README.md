# AWS Multi-Arch Image Build Action

## Overview

This repository provides a reusable GitHub Actions workflow to build and push multi-architecture Docker images to Amazon Elastic Container Registry (ECR). It simplifies the process of creating and publishing images that support multiple CPU architectures, such as `amd64` and `arm64`.

## Features

- **Multi-Architecture Support**: Build Docker images for multiple architectures.
- **AWS ECR Integration**: Push images directly to your AWS ECR repository.
- **Docker Build Cache**: Optional support for Docker build caching to speed up builds.
- **Metadata Labels**: Add custom labels to your Docker images.
- **Flexible Configuration**: Customize build arguments, platforms, and more through inputs.

## Usage

### 1. Create a Workflow in Your Repository

Add a new GitHub Actions workflow file (e.g., `.github/workflows/build-and-push.yml`) in your repository:

```yaml
name: Build and Push Multi-Arch Image to AWS ECR

on:
  push:
    branches:
      - main  # or your default branch

jobs:
  build-and-push:
    uses: ka-nabellinc/aws-multiarch-image-build-action/.github/workflows/multiarch-image-build-action.yml@main
    with:
      repo-url: <AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com/<your-repo>
      tag: latest
      file: ./Dockerfile
      aws-region: ap-northeast-1
      aws-access-key-id: <AWS_ACCESS_KEY_ID>
      platforms: |
        [
          {"arch": "amd64", "runner": "ubuntu-22.04"},
          {"arch": "arm64", "runner": "ubuntu-22.04-arm64"}
        ]
      cache-from: type=registry,ref=<AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com/<your-repo>:latest
      cache-to: type=inline
    secrets:
      aws-secret-access-key: <AWS_SECRET_ACCESS_KEY>
      build-args: |
        HOGE=FUGA
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.
