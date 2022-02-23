# Setup Instructions

change to revert!

## Setup Permissions

* Create a GitHub App with `Read & write` access to the `Contents`
  permission.
* Download the app's private key.

  * **WARNING**: Treat this private key like a password! Anyone in
    posession of it can access and change the contents of the
    repositories the app has been installed on.

* Install the app on the repository with the wiki source and on the
  repository whose wiki will contain the deployed documentation.
* To both repositories, add the following secrets:

  * `APP_ID`: The ID for your GitHub App
  * `APP_PRIVATE_KEY`: A private key for your GitHub App in PEM format.

* Delete the private key from your machine. If you need to add the key
  to a new repository secret in the future, you can just generate a new
  key.

## Customize Script

Before using the scripts in this repository, you will need to replace:

* `test-wiki-revert` with the name of your GitHub App
* `97997431` with the User ID of your GitHub bot. You can retrieve this
  ID from `https://api.github.com/users/test-wiki-revert[bot]`,
  replacing `test-wiki-revert` with your GitHub App's name.
* `test-oppia` with the deployment repository.
* `test-oppia-docs` with the source repository.
* `U8NWXD` with your organization name.

## Add the Scripts

* Make sure both the source and deployment repositories exist. This
  means that the repository whose wiki you will be using as the
  deployment destination must have some wiki content so that the wiki
  repository exists.
* Add the revert workflow to the deployment repository.
* Add the deployment workflow to the source repository.
