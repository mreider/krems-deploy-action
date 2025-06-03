# krems-deploy-action

Builds and deploys static sites using [Krems](https://github.com/mreider/krems) to GitHub Pages.

## Usage

```yaml
name: Deploy Krems Site
on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pages: write
      id-token: write

    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Recommended for gh-pages deployments

      - name: Build and Deploy with Krems
        uses: mreider/krems-deploy-action@vX.Y.Z # Replace with the latest version
        # No 'with' block is needed as inputs for publish_dir and publish_branch have been removed.
        # The action now automatically:
        # 1. Expects the 'krems' binary to build the site into a './tmp' directory.
        # 2. Publishes the content of this './tmp' directory.
        # 3. Deploys to the 'gh-pages' branch.
```

**Note:** As of version `X.Y.Z` (replace with the new version number), the `publish_dir` and `publish_branch` inputs have been removed. The action now defaults to publishing the Krems build output (expected in `./tmp`) to the `gh-pages` branch.

## Requirements

- Repository must contain a config.yaml file for Krems configuration
- GitHub Pages must be enabled for the repository
