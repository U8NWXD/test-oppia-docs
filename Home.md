# Setup Instructions

## Setup Permissions

* Create a GitHub App with `Read & write` access to the `Contents`
  permission.
* Install the app on the repository with the wiki source and on the
  repository whose wiki will contain the deployed documentation.
* To both repositories, add the following secrets:

  * `APP_ID`: The ID for your GitHub App
  * `APP_PRIVATE_KEY`: A private key for your GitHub App in PEM format.

## Customize Script

Before using the scripts in this repository, you will need to replace:

* `test-wiki-revert` with the name of your GitHub App
* `97997431` with the User ID of your GitHub bot. You can retrieve this
  ID from `https://api.github.com/users/test-wiki-revert[bot]`,
  replacing `test-wiki-revert` with your GitHub App's name.
* `test-oppia` with the deployment repository.
* `test-oppia-docs` with the source repository.
* `U8NWXD` with your organization name.
