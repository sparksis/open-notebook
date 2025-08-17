# Flux Configuration for Open Notebook

This directory contains the Kubernetes manifests for deploying Open Notebook with Flux CD.

## Overview

The manifests in this directory are designed to be consumed by an external Kustomization resource.
This allows for easy integration with existing Flux setups and enables the use of variables for environment-specific configurations.

## Resources

The following resources are included:

-   `kustomization.yaml`: Defines the Kustomization for the flux resources.
-   `deployment.yaml`: Defines the `Deployment` resource for the `open-notebook` application.
-   `service.yaml`: Defines the `Service` resource to expose the `open-notebook` application.

## Usage

To use these manifests, create a `Kustomization` resource in your Flux setup that points to this directory.
You can override the default values by using patches in your `Kustomization` resource.

## Configuration

The deployment uses `envFrom` to load environment variables from a secret named `open-notebook-secret`.
You need to create this secret in the same namespace as the deployment.

Here is an example of how to create the secret:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: open-notebook-secret
type: Opaque
stringData:
  # SECURITY
  OPEN_NOTEBOOK_PASSWORD: "your-secure-password"

  # OPENAI
  OPENAI_API_KEY: "your-openai-api-key"

  # ANTHROPIC
  ANTHROPIC_API_KEY: "your-anthropic-api-key"

  # ... and so on for all the other environment variables
```

## Volumes and Persistent Storage

The deployment uses `hostPath` volumes to persist data.
**This is not recommended for production environments.**
You should update the `deployment.yaml` to use `PersistentVolumeClaim` for production.

The following volumes are defined:

-   `notebook-data`: Stores the application data. Mapped to `/app/data` in the container.
-   `surreal-data`: Stores the SurrealDB data. Mapped to `/mydata` in the container.

You need to update the `hostPath` in the `deployment.yaml` to point to the actual paths on your host machine.
