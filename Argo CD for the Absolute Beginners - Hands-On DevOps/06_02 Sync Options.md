# Sync Options in Argo CD

Hello everyone. In this lecture, we will understand some of the important options available while deploying applications in Argo CD.

When you click on New App, you provide the application name and project name. If you scroll down, you will see something called sync options.

There are six sync options available. Let us understand them one by one.

## 1. Skip Schema Validation

In Kubernetes, we usually use the `kubectl apply` command with manifest files to deploy resources. However, there are certain Kubernetes resource types where you may need to add another parameter called `--validate=false`.

If you have such resource types, like Service Catalog, you can skip validation. So, skip schema validation means we will not use `kubectl apply` with the `--validate=false` parameter.

## 2. Auto-create Namespace

This is something we have seen in our previous demo. If you specify a namespace name and want Argo CD to create it for you, you can enable this option.

## 3. Prune Last

This feature helps us prune resources at the final stage. If you select `prune last`, Argo CD will deploy the resources, and once everything is done, it will delete the resources at the final step.

## 4. Apply Out of Sync

Let us say we have multiple files in a manifest, and only one file has changes. If you want to apply changes only to those resources where the code has changed, you can use apply out of sync.

In this case, only the manifest files that are out of sync will be applied, and anything already in sync will not be touched.

## 5. Respect Ignore Differences

Assume we have two files in Git: a namespace and a deployment. If changes are made to a deployment, such as increasing the replica count to three, Argo CD detects the change as out of sync.

If during synchronization someone else changes the replicas to five, Argo CD will first apply the initial change, show it as out of sync again, and then apply the second change.

## 6. Server-Side Apply

By default, Argo CD executes resources using the client-side apply method. However, for some workloads, you may want to use server-side apply for better conflict handling and more advanced Kubernetes behavior.

This option allows Kubernetes to apply changes on the server side rather than only through the client context.

These sync options help you control how Argo CD handles deployment, validation, drift, and update behavior in a flexible and efficient way.

That is it for this topic. Let us move on to the next part.
