# VEDA QHub

This repo hosts the configuration required to deploy a QHub for VEDA.

## Pre-requisites

* AWS: This service is currently being deployed to the VEDA Dev AWS Account (managed by UAH). You will need access to that AWS account to deploy.
* QHub CLI:

```sh
pip install qhub==0.4.3
```

## Deployment

* Setup [Github OAuth App](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app).

NOTE: Your Github OAuth app must have the appropriate callback URL: https://docs.qhub.dev/en/stable/source/admin_guide/breaking-upgrade.html#update-oauth-callback-url-for-auth0-or-github

* Set environment variables GITHUB_TOKEN (from your github account), AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY (from UAH AWS account)
* Create a config file (Skip this step unless you want to create a new config file):

    ```bash
    qhub init aws --project veda-qhub --domain veda-analytics.delta-backend.com \
    --ci-provider github-actions --auth-provider github \
    --repository github.com/NASA-IMPACT/veda-qhub
    ```

    This will create a config.yaml file with all the configuration you need to deploy. However, it will need to be populated with values for your Github OAuth app and an initial root password for keycloak under `security` and other sections may require inspection and update as well. Compare with qhub-config.yaml in this repository.

* Deploy `qhub deploy -c qhub-config.yaml`
* Add CNAME record in Route53 for the domain in the config.yaml file

