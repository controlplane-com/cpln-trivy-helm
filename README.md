# cpln-trivy-scan

## Purpose

Scan images in the org's image repository and store trivy reports in S3. The URL to the scanned image report is stored as a tag on each image, accessible from the Control Plane UI.

## Prerequisites

- An org in cpln
- An AWS account registered in cpln
- A Control Plane Service Account named "cpln-trivy-service-account" with a key called key1. Make sure to note the key's value as you will not be able to access it later from the UI.
- Store the key you received in the above step in an opaque secret called "trivy-password"
  

## Installation

Make sure your cpln profile is pointing to the correct org and that you're signed in as superuser.

To Install:

Only edit the file cpln-trivy/values.yaml file to set all the values.

```
cpln helm install cpln-trivy
```

To Uninstall:

```
cpln helm uninstall cpln-trivy
```


## Misc.

To clear all the tags from the images, perform the following:

```
cpln image query --tag cpln/trivy-scan -o json | jq ".items[].name" | xargs cpln image tag --remove cpln/trivy-scan

cpln image query --tag cpln/trivy-scan-time -o json | jq ".items[].name" | xargs cpln image tag --remove cpln/trivy-scan-time

```
