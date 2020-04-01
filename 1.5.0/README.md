# Overview

This is a poc using Istion 1.5.1

# Prerequisites

* Kubernetes Cluster

* Kubectl

* Istioctl

# Setup

Install Istio

`istioctl manifest apply --set profile=demo`

Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later:

`kubectl label namespace default istio-injection=enabled`

Deploy the sample application

`kubectl apply -f bookinfo.yaml`

The application will start. As each pod becomes ready, the Istio sidecar will deploy along with it.

`kubectl get services,pods`

```
Re-run the previous command and wait until all pods report READY 2 / 2 and STATUS Running before 
you go to the next step. This might take a few minutes depending on your platform.
```

Verify everything is working correctly up to this point. Run this command to see if the app is running inside the cluster and serving HTML pages by checking for the page title in the response:

`kubectl exec -it $(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}') -c ratings -- curl productpage:9080/productpage | grep -o "<title>.*</title>"`

# Cleanup

