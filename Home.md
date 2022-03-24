## Setup Instructions

### Setup Permissions

* Create a GitHub App with the following settings
  ([docs](https://docs.github.com/en/developers/apps/building-github-apps/creating-a-github-app)):

  * `Name` and `Description` that describe the app's purpose.
  * For `Homepage URL` you can just put the link to your documentation
    source repository. This URL is required by GitHub, but we don't use
    it for anything.
  * Leave `Callback URL`, `Setup URL`, `Webhook URL`, and `Webhook secret` blank.
  * We don't use user authorization tokens, so you can leave `Expire
    user authorization tokens` checked and leave `Request user
    authorization (OAuth) during installation` and `Enable Device Flow`
    unchecked.
  * We don't use webhooks, so leave the `Active` checkbox under
    `Webhook` unchecked.
  * Give `Read & write` access to the `Contents` permission.
  * Don't subscribe to any events.
  * Allow installation `Only on this account` since we don't expect this
    app to be used outside of the organization.

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

### Customize Script

Before using the scripts in this repository, you will need to replace:

* `test-wiki-revert` with the name of your GitHub App
* `97997431` with the User ID of your GitHub bot. You can retrieve this
  ID from `https://api.github.com/users/test-wiki-revert[bot]`,
  replacing `test-wiki-revert` with your GitHub App's name.
* `test-oppia` with the deployment repository.
* `test-oppia-docs` with the source repository.
* `U8NWXD` with your organization name.

### Add the Scripts

* Make sure both the source and deployment repositories exist. This
  means that the repository whose wiki you will be using as the
  deployment destination must have some wiki content so that the wiki
  repository exists.
* Add the revert workflow to the deployment repository.
* Add the deployment workflow to the source repository.

## Security Analysis

This approach introduces the following security concerns:

* The permissions for the documentation source repository must be
  maintained as they no longer automatically follow the deployment
  repository permissions.
* Access to the GitHub App must be secured. In particular, the app
  should be created at the organization level, and the minimum number of
  people should be granted [app manager
  permissions](https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization#github-app-managers). Organization owners automatically have access.
* The GitHub App's credentials must also be secured. In particular,
  there should be no copies of the private key outside of GitHub actions
  secrets.

Here are some alternative approaches:

* Creating a new user account that we can give access to the necessary
  repositories and who the scripts will act as.

  * This means we have to keep track of securing another account and
    that account's credentials. The GitHub App approach is better
    because we can use existing GitHub accounts to manage the app, and
    it's not possible to log in as the app.
  * The app's actions are clearly marked as being by a bot, which is
    better than a user account which will look like a human user.

* Using a personal access token (PAT).

  * The PAT grants broad access across all the repositories the user who
    generated the PAT has privileges for. This introduces a risk that a
    compromise of Oppia could grant an attacker access to other,
    unaffiliated repositories. A GitHub App has more fine-grained
    permissions that can be restricted to particular repositories.

* Using the `GITHUB_TOKEN` generated automatically for actions
  workflows.

  * This token does not grant access to the wiki, so even if we
    force-deployed from the source repository instead of creating a
    revert commit, the workflow in the deployment repository that
    detects an edit through the web interface would not have permission
    to force-deploy the source documentation to the deployment wiki.
