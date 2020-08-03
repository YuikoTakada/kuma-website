# Helm

Kuma support a fully automated way to manage its deplyment lifecycle on Kubernetes through [helm charts](https://kumahq.github.io/charts).

### Adding the Kuma charts repo

Follow this simple command to add the Kuma charts repository to your local helm deployment:

```bash
helm repo add kuma https://kumahq.github.io/charts
```

### Installing the basic standalone mode

Note that the Helm charts assume that the `kuma-system` namespace is existing already

```bash
kubectl create namespace kuma-system
helm upgrade -i kuma kuma/kuma
```

The default namespace can be overridden with `--set global.namespace=other-kuma-system`

### Installing Kuma in a distribute mode

The provided Helm charts, do support installing Kima in a [`Distribute Mode`](../../documentation/deployments/#distributed-mode).

To install the Global Control Plane, just set the `controlPlane.mode` value to `global` when installing the chart. That can be in a provided values file or on the command line:
```bash
helm install kuma --set controlPlane.mode=global kuma/kuma
```

Similarly, to install the Remote Control plane we need to provide `controlPlane.mode=remote`,`controlPlane.zone=<zone-name>` and `controlPlane.kdsGlobalAddress=grpcs://<global-kds-address>`

```bash
helm install kuma --set controlPlane.mode=remote,controlPlane.zone=zone-1,controlPlane.kdsGlobalAddress=grpcs://<global-kds-address>  kuma/kuma
```

For more information on the available parameters fetch the README content from the chart in the Helm repo:

```bash
helm show readme kuma/kuma
```