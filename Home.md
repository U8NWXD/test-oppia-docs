# Setup Instructions

## Setup Access Tokens

* Create a GitHub App with `Read & write` access to the `Contents`
  permission.
* Install the app on the repository with the wiki source and on the
  repository whose wiki will contain the deployed documentation.
* To both repositories, add the following secrets:

  * `APP_ID`: The ID for your GitHub App
  * `APP_PRIVATE_KEY`: A private key for your GitHub App in PEM format.
