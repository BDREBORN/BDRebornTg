---
tag: [ "codenvy" ]
title: Version Control
excerpt: ""
layout: docs
permalink: /:categories/version-control/
---
{% include base.html %}

**Applies To**: Codenvy on-premises installs.

Codenvy is powered by the open Eclipse Che project. You will see references to Eclipse Che and its documenation below.
---

Public or private repositories are used to import projects into workspaces, to use the Git / Subversion menus, and to use and create [Factories]({{base}}/docs/integration-guide/workspace-automation/index.html). Some repository tasks such as git push and access to private repositories require setting up SSH or oAuth authentication mentioned below.

# Using SSH  
Setup of an SSH keypair is done inside each user's workspace. Refer to [git docs]({{base}}{{site.links["ide-git-svn"]}}) for additional information. Setting up SSH keypairs inside a workspace must be done prior to being able to use private repository URLs.

Refer to specific [GitHub]({{base}}{{site.links["ide-git-svn"]}}#github-example) and [GitLab]({{base}}{{site.links["ide-git-svn"]}}#gitlab-example)) SSH examples on how to upload public keys to these repository providers.

For other git-based or SVN-based repository providers, please refer to their documentation for adding SSH public keys.

# Using oAuth  
## GitLab oAuth
Currently it's not possible for Codenvy to use oAuth integration with GitLab. Although GitLab supports oAuth for clone operations, pushes are not supported. You can track [this GitLab issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/18106) in their issue management system.

## BitBucket Server oAuth
You can setup oAuth to a dedicated BitBucket Server.
#### 1. Generate Keys
SSH to your BitBucket Server instance and generate RSA key-pairs
```shell
# generate the key pairs
$ openssl genrsa -out private.pem 1024

# copy the key and pem to a location where it can be accessed
$ openssl rsa -in private.pem -pubout > public.pub`
$ openssl pkcs8 -topk8 -inform pem -outform pem -nocrypt -in private.pem -out privatepkcs8.pem 
```
#### 2. Setup Codenvy in BitBucket Server
In the Bitbucket Server as an Admin:

1. Go to Administration -> Application Links
2. Enter your Codenvy URL in the 'application url' field and press the 'Create new link' button.
3. When  the 'Configure Application URL' window appears press the 'Continue' button.
4. In the ‘Link applications’ window fill in the following fields and press the 'Continue' button:
  - Application Name : Codenvy
  - Service Provider Name : Codenvy
  - Consumer key : {added by you} (Save this string, you will need it later)
  - Shared secret : {added by you} 
  - Request Token URL : {your Bitbucket Server URL}/plugins/servlet/oauth/request-token
  - Access token URL : {your Bitbucket Server URL}/plugins/servlet/oauth/access-token
  - Authorize URL : {your Bitbucket Server URL}/plugins/servlet/oauth/authorize

#### 3. Add Codenvy oAuth Info
In the following screen press the pencil icon to edit and select the 'Incoming Authentication' menu. Fill in the following fields in the ‘OAuth’ tab:
- Consumer Key : {the consumer key from the previous step}
- Consumer Name : Codenvy
- Public Key : {the key from public.pub file} (The key must not contain ‘-----BEGIN PUBLIC KEY-----’ and ‘-----END PUBLIC KEY-----’ rows)
- Consumer Callback : {your Codenvy URL>}/api/oauth/1.0/callback

#### 4. Configure Codenvy Properties
In the `codenvy.env` file add (or change if they already exist):
- bitbucket_consumer_key : the consumer key you have entered before
- bitbucket_private_key : the key from privatepkcs8.pem file 
- (The key must not contain ‘----BEGIN PRIVATE KEY-----’ and ‘-----END PRIVATE KEY-----’ rows) (The key must be specified as a single raw)
- bitbucket_endpoint : replace the default Bitbucket url by your Bitbucket Server url

#### 5. Restart Codenvy
Restart your Codenvy server to enable the integration.

## GitHub oAuth
### Setup oAuth at GitHub
1. Register an application in your GitHub account. Refer to [Setup oAuth at GitHub]({{base}}{{site.links["ide-git-svn"]}}#github-oauth) for additional information.
2. Update the `codenvy.env` with secret, ID and callback:
```text  
oauth.github.clientid=yourClientID
oauth.github.clientsecret=yourClientSecret
oauth.github.authuri=https://github.com/login/oauth/authorize
oauth.github.tokenuri=https://github.com/login/oauth/access_token
oauth.github.redirecturis=http://$hostname/wsmaster/api/oauth/callback
```
After the above steps, execute `puppet agent -t`.

### Using GitHub oAuth
With oAuth setup you can perform all git actions with the repo, including commits and pushes. You can also use the Codenvy pull request panel (found on the far right of pull-request enabled workspaces).

# Git and Subversion Workspace Clients
After importing a repository, you can perform the most common Git and SVN operations using interactive menus or through console commands.

**Note: Use of git menu remote push command will not work prior setting up SSH or oAuth authentication.**
![git-menu.png]({{base}}/docs/assets/imgs/codenvy/git-menu.png)

![svn-menu.png]({{base}}/docs/assets/imgs/codenvy/svn-menu.png)

# Built-In Pull Request Panel
Within the Codenvy IDE there is a pull request panel to simplify the creation of pull requests for GitHub, BitBucket or Microsoft VSTS (with git) repositories.
