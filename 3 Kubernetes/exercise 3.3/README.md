# Exercise 3.3: Creating and Querying Deployments and Pods

In this exercise, you will specify a deployment (supervisor) for your pod by defining a deployment manifest (`deployment.yaml`). This manifest will be applied to your Kubernetes cluster to create a deployment resource, which automatically creates a pod. This pod is then running your container. Finally, you will delete the pod managed by a deployment in order to see that Kubernetes takes care of creating it again.

## Instructions

1. Create a file `deployment.yaml` with the following content:

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: demo
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: demo
      template:
        metadata:
          labels:
            app: demo
        spec:
          containers:
          - name: demo
            image: agrimmer/demo:time
            ports:
            - containerPort: 8888
    ```

1. Apply the *deployment* to your Kubernetes cluster using: 

    ```console
    kubectl apply -f deployment.yaml
    kubectl apply -f https://raw.githubusercontent.com/danielraso7/ws22/main/3%20Kubernetes/exercise%203.3/deployment.yaml
    ```

1. You can see all your active deployments (in your current namespace) by executing:

    ```console
    kubectl get deployments
    ```

    ```source
    NAME   READY   UP-TO-DATE   AVAILABLE   AGE
    demo   1/1     1            1           10m
    ```

1. To get more information on the `demo` deployment use:

    ```console
    kubectl describe deployment demo
    ```

1. To forward your local port **9999** to the container port **8888**, use:

    ```console
    kubectl port-forward deployment/demo 9999:8888
    ```

    :mag: Now, access the website [http://localhost:9999](http://localhost:9999). What is shown there? 

1. Query the *pods* of your *deployment* with:
    
    ```console
    kubectl get pods
    ```

    ```source
    NAME                    READY   STATUS    RESTARTS   AGE
    demo-bd8fd986b-as7dmf   1/1     Running   0          2m
    ```

1. Delete the *pod* with:
    
    ```console
    kubectl delete pod --selector app=demo
    ```

1. Now, query the *pods* of your *deployment* again:
    
    ```console
    kubectl get pods
    ```

    :mag: What is your observation? 

1. Increase the number of replicas to 3. Research at least two different approaches.

ANSWER: change deployment.yaml (on own fork) to "replicas: 3" or execute some command (which leads to the vim) in the command line (gcloud) (ask Grimmer)