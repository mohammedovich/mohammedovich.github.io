---
title: Demystifying Kubernetes: CRDs, Custom Resources, and the Reconciliation Loop
subtitle: "From Definition to Deletion — How Kubernetes CRDs, Custom Resources, and Operators Work Together :zap:"
summary: This post breaks down Kubernetes’ extensibility through Custom Resource Definitions (CRDs) and Custom Resources (CRs), showing how they’re applied, how controllers and operators run reconciliation loops to enforce desired state, and how finalizers ensure safe, graceful deletion of resources. Includes a lifecycle diagram to make the process clear.
date: 2025-08-09
cardimage: image.jpeg
featureimage: image.jpeg
caption:       
authors:
  - Mohammed: author.png
---

#
Kubernetes isn’t just about Pods, Deployments, and Services—it’s a framework for building powerful, extensible APIs. And at the heart of that extensibility are Custom Resource Definitions (CRDs), Custom Resources (CRs), and the controllers/operators that breathe life into them.

If you’ve ever wondered how CRDs get applied, how controllers “magically” keep resources in sync, and what happens when they’re deleted, this post will walk you through the full lifecycle—from YAML to reconciliation to finalization.

## 1. CRDs: Extending the Kubernetes API

**Custom Resource Definitions (CRDs)** Custom Resource Definitions (CRDs) are Kubernetes’ way of letting you define new API objects—your own resource types—without modifying Kubernetes’ core code.

For example, you might create a CRD called Backup that represents a database backup job. Once the CRD is registered, you can create Backup resources in your cluster just like you create Pods or Deployments.

Here’s a simple CRD snippet:

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: backups.example.com
spec:
  group: example.com
  names:
    kind: Backup
    plural: backups
    singular: backup
  scope: Namespaced
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                database:
                  type: string
                schedule:
                  type: string
```

Once this CRD is applied:

```bash
kubectl apply -f backup-crd.yaml
```

Now Kubernetes knows about a new resource type: backups.example.com.

```bash
kubectl get backups
kubectl describe backup my-daily-backup
```

## 2. Custom Resources: Instantiating Your API

**Custom Resource (CR)** is an actual instance of your new type—like a Pod is an instance of PodSpec.

Example Backup CR:

```yaml
apiVersion: example.com/v1
kind: Backup
metadata:
  name: my-daily-backup
spec:
  database: postgres-prod
  schedule: "0 2 * * *"
```

You apply it with:

```bash
kubectl apply -f backup-cr.yaml
```

At this stage, the resource exists in etcd (Kubernetes’ data store), but it doesn’t actually do anything yet. That’s where controllers/operators step in.

## 3. Controllers & Operators: The Brain Behind the API

A controller in Kubernetes is a process that watches the API server for changes to resources and takes action to move the cluster towards the desired state.

When we talk about Operators, we’re usually talking about a controller + domain-specific logic to manage complex applications (databases, message queues, etc.).

Here’s how it works under the hood:

1. **Watch**: The controller subscribes to resource events (```ADDED```, ```MODIFIED```, ```DELETED```) using the Kubernetes API.

2. **Queue**: When something changes, it’s queued for processing.

3. **Reconcile**: The controller runs a reconciliation loop, comparing the desired state (your CR spec) with the current state (the real world), then making adjustments.

4. **Repeat**: The loop is continuous—Kubernetes never assumes the world is in the right state.

## 4. The Reconciliation Loop in Action

Imagine you created the ```Backup``` CR above. The reconciliation loop might:

- Check if a CronJob exists for ```postgres-prod``` at 2 AM.
- If not, create it.
- If it exists but the schedule is wrong, update it.
- If the database name changed, trigger a redeployment of the backup job.

This loop ensures eventual consistency—even if something breaks or gets deleted outside Kubernetes, the controller will put it back to match the CR’s spec.

A simplified pseudocode example:

```go
func Reconcile(backup Backup) {
    if !cronJobExists(backup) {
        createCronJob(backup)
    } else if scheduleChanged(backup) {
        updateCronJob(backup)
    }
}
```

## 5. Finalizers: Graceful Deletion

When you delete a CR, Kubernetes doesn’t immediately remove it from etcd if it has a finalizer. Instead:

1. The deletion timestamp is set.
2. The controller sees the resource is “pending deletion”.
3. The controller runs clean-up logic (e.g., delete backup files from cloud storage).
4. The controller removes the finalizer from the resource.
5. Kubernetes completes the deletion.

Example finalizer in a CR:

```yaml
metadata:
  finalizers:
    - backups.example.com/finalizer
```

This ensures external resources aren’t left dangling when the CR is removed.

## 6. Bringing It Together

The lifecycle looks like this:

```perl
CRD applied  →  CR created  →  Controller reconciles state  
   ↓                ↓                ↓
API extended   Desired state    World matches
               declared         desired state
```

And when deleting:

```cpp
kubectl delete CR  →  Finalizer runs  →  Resource gone
```

## 7. Why This Matters for Cloud Engineers & DevOps

Understanding ```CRDs```, ```CRs```, and the ```reconciliation```/```finalization``` process lets you:

- Build custom Kubernetes APIs for your org’s workflows.
- Automate operational tasks (backups, scaling, provisioning).
- Safely clean up external resources without manual intervention.
- Debug operator behavior when things go wrong.

At its core, Kubernetes is not just an orchestrator—it’s a control loop platform. Mastering CRDs and controllers turns Kubernetes into a programmable, self-healing infrastructure layer.