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
