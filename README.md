# Simple helm chart for CVAT

Features:

- creates a superuser and store it in a secret for integration with other kubernetes resources
- optionally uses zalando's postgres operator (see [here](zalando-pgo.md))

## Usage

See [here](charts/cvat-helm/README.md) for all configuration options

```shell
helm repo add cvat-helm https://sebagarayco.github.io/cvat-helm/

# list the versions available
helm search repo cvat-helm

# check what settings are available
helm inspect values cvat-helm/cvat-helm

# install
helm install cvat cvat-helm/cvat-helm \
        --namespace='cvat' --create-namespace \
        --set superUser.initialPassword=boo \
        --set ingress.host=cvat.com \
        --set ingress.clusterIssuer=letsencrypt-prod
        # optionally AWS
        --set ingress.certificateArn="<certificate_arn>" \
        --set ingress.cognitoEnabled="true" \
        --set ingress.cognitoUserPool="<poolId>" \
        --set ingress.cognitoUserPoolClient="<poolClient>" \
        --set ingress.cognitoUserPoolDomain="<poolDomain>"
```
