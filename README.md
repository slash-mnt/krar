# Kubernetes Resources Auto Rollouter
krar is a simple chart intended to refresh images using floating tags on selected resources.
Can be considered as a light Keel alternative.

The main use case is when your Kubernetes cluster is running applications/services using major or minor image
versions (floating tags) and you want the most updated.

> [!WARNING] Triggering that effect can affect resource availability if:
> * There is only one replica of the resource,
> * The image version is too open like `latest`.

> [!IMPORTANT]
> Only resources with `imagePullPolicy` set to `Always` will work.

It's possible to defined multiple jobs to handle resources to rollout in specific ways.

## What's inside?

**No dependency required.**

* ServiceAccount
* CluterRole/ClusterRoleBinding with GET, PATCH and LIST permissions on `""`, `"apps"` (deployments, daemonsets, statefulsets only)
* As many CronJob you need

## How to mark my resource for automatic rollout?

With default values, you can add the following label on your `Deployment`, `DaemonSet` and `StatefulSet` resources:

```yaml
slash-mnt.com/enable-autorollout: once-a-month
```

to allow autorollout using the job named `once-a-month`.