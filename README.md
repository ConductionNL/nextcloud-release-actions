# Release Workflow

This GitHub Actions workflow automates the release process for a Nextcloud app.

## What it does

1. **Version Management**:
   - Extracts the current version from `appinfo/info.xml`
   - Increments the patch version
   - Updates `info.xml` with the new version

2. **Build Process**:
   - Sets up Node.js and PHP environments
   - Installs npm and Composer dependencies
   - Runs build scripts

3. **Package Creation**:
   - Copies relevant files to a package directory
   - Creates a tarball (`nextcloud-release.tar.gz`)
   - Signs the tarball

4. **Release Creation**:
   - Generates a changelog
   - Creates a new GitHub release with the tarball
   - Tags the release with the new version

5. **Nextcloud App Store**:
   - Uploads the app to the Nextcloud App Store

## Triggers

- Push to `master` or `main` branch
- Manual trigger with optional version input

## Requirements

- GitHub repository secrets:
  - `NEXTCLOUD_SIGNING_CERT`
  - `NEXTCLOUD_SIGNING_KEY`
  - `NEXTCLOUD_APPSTORE_TOKEN`

## Usage

The workflow runs automatically on push to main branches. For manual triggers:

1. Go to Actions tab in your repository
2. Select "Release Workflow"
3. Click "Run workflow"
4. Optionally specify a version, or leave blank to use `info.xml` version

## Customization

Adjust the workflow as needed:
- Modify file exclusions in the rsync command
- Add or remove build steps
- Change the release branch in the "Git Version" step

Ensure all paths and commands are correct for your project structure.