# LFX KYVERNO

# Kyverno Policy and Exception Example

This repository contains examples of Kyverno policies and exceptions to demonstrate how to enforce and exempt Kubernetes resources from specific policies. In this example, we've create a Kyverno policy that limits the number of containers in a Pod and an exception for a specific Pod or Deployment.

## Kyverno Policy: Container Count Limit

The `Limit-Container` Kyverno policy enforces a maximum limit of two containers in a Pod. Any Pod with more than two containers will be blocked from creation.

To apply the policy, run the following command:

```bash
kubectl apply -f kyverno-policies/Limit-Container.yaml
```

## Kyverno Exception: Important App

The `exception-imp-app` Kyverno PolicyException grants an exception to a Pod or Deployment named important-app in the delta namespace. This exception allows the resource to bypass the container count limit policy.

To apply the exception policy, run the following command:

```bash
kubectl apply -f kyverno-policies/exception-imp-app.yaml
```
## Example Resources

The resource-examples folder contains example Kubernetes resource definitions for testing the policies.


example-pod-violation.yaml: A Pod that violates the container count limit policy by having three containers.

example-pod-created.yaml: A Pod that follows the container count limit policy having two containers.

important-app-pod.yaml: A Pod marked as an exception that is allowed to have more than two containers.


To create these example resources, run the following commands:

```bash
kubectl apply -f resource-examples/example-pod-violation.yaml
kubectl apply -f resource-examples/example-pod-created.yaml
kubectl apply -f resource-examples/important-app-pod.yaml
```

## Cleaning Up

To remove the resources and policies, you can use the kubectl delete command with the respective YAML files or delete the namespace if you've used a separate one for testing.

```bash
kubectl delete -f kyverno-policies/
kubectl delete -f resource-examples/
```

