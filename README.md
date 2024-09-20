# Nextcloud App Release Action

This GitHub Action automates the release process for Nextcloud apps. It handles version incrementing, building, packaging, signing, creating a GitHub release, and uploading to the Nextcloud App Store.

## Features

- Automatically increments the patch version
- Updates version in info.xml
- Commits and pushes version update
- Builds npm and Composer dependencies
- Creates a tarball of the app
- Signs the release
- Generates changelog
- Creates a GitHub release
- Uploads the app to the Nextcloud App Store
- Verifies the release contents

## Inputs

| Input | Description | Required |
|-------|-------------|----------|
| `github_token` | GitHub token for creating releases and pushing changes | Yes |
| `signing_cert` | Nextcloud signing certificate | Yes |
| `signing_key` | Nextcloud signing key | Yes |
| `appstore_token` | Nextcloud App Store token | Yes |

## Usage

To use this action in your workflow, add the following step:

```yaml
name: Release Nextcloud App
uses: your-username/nextcloud-app-release-action@v1
with:
github_token: ${{ secrets.GITHUB_TOKEN }}
signing_cert: ${{ secrets.NEXTCLOUD_SIGNING_CERT }}
signing_key: ${{ secrets.NEXTCLOUD_SIGNING_KEY }}
appstore_token: ${{ secrets.NEXTCLOUD_APPSTORE_TOKEN }}
```

## Workflow Example

Here's a complete workflow example:

```yaml
	name: Release Nextcloud App
on:
push:
branches:
main
workflow_dispatch:
jobs:
release:
runs-on: ubuntu-latest
steps:
name: Release Nextcloud App
uses: your-username/nextcloud-app-release-action@v1
with:
github_token: ${{ secrets.GITHUB_TOKEN }}
signing_cert: ${{ secrets.NEXTCLOUD_SIGNING_CERT }}
signing_key: ${{ secrets.NEXTCLOUD_SIGNING_KEY }}
appstore_token: ${{ secrets.NEXTCLOUD_APPSTORE_TOKEN }}


## Prerequisites

Before using this action, ensure that:

1. Your Nextcloud app repository is properly structured.
2. You have a valid signing certificate and key for Nextcloud app releases.
3. You have a valid Nextcloud App Store token.
4. Your `appinfo/info.xml` file is correctly formatted and contains a `<version>` tag.
5. You have the necessary GitHub secrets set up in your repository settings.

## Customization

The action uses sensible defaults for most Nextcloud apps. However, you may need to customize it for your specific needs:

- Modify the `rsync` exclusion list in the action if you have different files or directories to exclude.
- Adjust the Node.js or PHP versions if your app requires different versions.

## Notes

- This action will automatically increment the patch version of your app. If you need to update major or minor versions, you should do this manually before running the action.
- The action will commit and push changes to your repository, create a new tag, and create a GitHub release.
- Make sure your repository allows the GitHub Action to push commits (check your branch protection rules if you have any).

## Contributing

Contributions to improve this action are welcome. Please feel free to submit issues or pull requests.
