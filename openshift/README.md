# Installing Crossplane on OpenShift

## Installing the Crossplane runtime 

Instructions are based on [Crossplane docs](https://crossplane.io/docs/v1.1/getting-started/install-configure.html):

```shell
kubectl create namespace crossplane-system

helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update
```

For OpenShift, you need to setup the security context as follows:

```shell
helm install crossplane --namespace crossplane-system crossplane-stable/crossplane --set securityContextCrossplane.runAsUser=null --set securityContextCrossplane.runAsGroup=null --set securityContextRBACManager.runAsUser=null --set securityContextRBACManager.runAsGroup=null
```

## Installing Providers

Currently, providers on OpenShift should be installed with the provider yaml template as the Crossplane
CLI does not yet support the `ControllerConfig` which sets an empty security context so that OpenShift
handles `runAsUser` and `runAsGroup` as appropriate.

First, apply the controller config:

```shell
kubectl apply -f openshift-config.yaml
```

Then, install the IBM provider as follows:

```shell
kubectl apply -f provider-ibm-cloud.yaml
```

then follow the rest of the instructions to configure the provider e.g. [`ibm`](https://github.com/crossplane-contrib/provider-ibm-cloud#generate-ibm-cloud-api-key).

For other providers, e.g. `provider-aws`, install the provider with:

```shell
kubectl apply -f provider-aws.yaml
```

Then, follow the rest of the instructions to configure the provider e.g. [`aws`](https://crossplane.io/docs/v1.1/getting-started/install-configure.html#install-aws-provider)