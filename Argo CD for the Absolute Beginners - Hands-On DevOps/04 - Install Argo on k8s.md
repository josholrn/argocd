Tested versions: https://github.com/PacktPublishing/Argo-CD-for-the-Absolute-Beginners---Hands-On-DevOps

Argocd releases: https://github.com/argoproj/argo-cd/releases
  - choose the `latest` version - most stable
  - you can choose Non-HA or HA:
  - Non-HA:
    kubectl create namespace argocd
    kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/v3.5.3/manifests/install.yaml

After installing Non-HA, you can check the status of the pods:
  $ kubectl get all -n argocd

pod/argocd-server-xxx is the main Argo CD server pod, and it should be in a Running state. You can also check the logs of the pod to ensure that it has started correctly:
  $ kubectl logs -n argocd pod/argocd-server-xxx

argo-cd-server service is the main entry point for accessing the Argo CD web UI. 
You can expose it using a LoadBalancer or NodePort, depending on your cluster setup. 
For example, to expose it as a LoadBalancer:
  $ kubectl expose service argocd-server -n argocd --type=LoadBalancer --name=argocd-server-lb

For example, to expose it as a NodePort:
  $ kubectl expose service argocd-server -n argocd --type=NodePort --name=argocd-server-np

or using `kubectl edit svc argocd-server -n argocd` and change the `type` to `NodePort` and after that you should see the NodePort assigned to the service like the following output:

  $ kubectl get svc argocd-server -n argocd
  NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                                     AGE
  argocd-server   NodePort    10.110.71.193   <none>        80:31978/TCP, 443:32000/TCP                 5m

To display all the api resources in the argocd namespace, you can use the following command:
  $ kubectl api-resources -n argocd

showing:
  - applications
  - appprojects
  - applicationsets

With that we can check the objects like:
  $ kubectl get applications -n argocd
  $ kubectl get appprojects -n argocd
  $ kubectl get applicationsets -n argocd

You usually install everything in the argocd namespace, but you can also install it in a different namespace if you prefer. Just make sure to change the namespace in the commands accordingly.
  $ kubectl create namespace my-argocd
  $ kubectl apply -n my-argocd --server-side --force-conflicts

  or

  $ kubectl get ns # and check the `argocd` namespace is created

Check the secrets in argocd namespace:
  $ kubectl get secrets -n argocd

  Usually you'll see:
  - argocd-initial-admin-secret  #this is where we get the initial password for the admin user
  - argocd-notifications-secret
  - argocd-secret
  - argocd-redis

