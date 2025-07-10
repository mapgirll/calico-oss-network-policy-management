# Module 1 - Getting Started with Calico Whisker

## Prerequisites
A Calico Open Source cluster, version 3.30+.

## Monitor network traffic in Calico Whisker

The Whisker web console deploys automatically, but it is not accessible from outside the cluster by default.
To view the web console, you need to allow access.

In this step, you will:

* **Set up port forwarding:** This allows you to access the Whisker web console from your browser.
* **Open the Whisker web console:** View the network traffic logs in real time.

1. Check that you have Calico Open Source 3.30 or greater installed, and that Calico Whisker is running in your cluster:

   ```bash
   kubectl get clusterinfo -o yaml
   ```

You are looking for the `calicoVersion` to be 3.30 or greater:

```bash,nocopy
  spec:
    calicoVersion: v3.30.2
```

2. Check that Calico Whisker is running:

```bash
kubectl get pod -A | grep whisker
```

```bash,nocopy
calico-system        whisker-7557ccb558-hvngj                       2/2     Running
```

```bash
kubectl get svc -A | grep whisker
```
```bash,nocopy
calico-system      whisker                           ClusterIP   10.96.153.8     <none>        8081/TCP
```

Calico Whisker should be running in the cluster on port 8081.

3. From your terminal, run the following command:

   ```bash
   kubectl port-forward -n calico-system service/whisker 8081:8081
   ```

   ```bash title="Expected output"
   Forwarding from 127.0.0.1:8081 -> 8081
   Forwarding from [::1]:8081 -> 8081
   ```

   Keep this terminal open throughout the rest of this workshop. Open a new terminal window or tab to continue.
   The Whisker web console needs the port forwarding to be active to receive logs.

4. To open Calico Whisker, open your browser and go to `localhost:8081`.
   You won't see any flows at the beginning.
   But in a few moments, as the console receives flow logs, you'll begin to see a list of connections.

   <Screenshot src="/images/calico-whisker.png" alt="Whisker" />
   *Figure {figCount++}: Whisker web console with allowed flows for core Kubernetes services.*

   The web console accumulates flow logs in real time.
   Keep this window open through the rest of the tutorial to see logs of the connections your pods are making.

## Deploy NGINX and BusyBox to generate traffic

Now it's time to generate some network traffic.
We'll do this first by deploying an NGINX server and exposing it as a service in the cluster.
Then we'll make HTTP requests from another pod in the cluster to the NGINX server and to an external website.
For this we'll use the BusyBox utility.

In this step, you will:
* **Create a server:** Deploy an NGINX web server in your Kubernetes cluster.
* **Expose the server:** Make the NGINX server accessible within the cluster.
* **Test connectivity:** Use a BusyBox pod to verify connections to the NGINX server and the public internet.

1. Create a namespace for your application:

   ```bash
   kubectl create namespace quickstart
   ```
   ```bash title="Expected output"
   namespace/quickstart created
   ```

2. Deploy an NGINX web server in the `quickstart` namespace:

   ```bash
   kubectl create deployment --namespace=quickstart nginx --image=nginx
   ```
   ```bash title="Expected output"
   deployment.apps/nginx created
   ```

3. Expose the NGINX deployment to make it accessible within the cluster:

   ```bash
   kubectl expose --namespace=quickstart deployment nginx --port=80
   ```
   ```bash title="Expected output"
   service/nginx exposed
   ```

4. Start a BusyBox session to test whether you can access the NGINX server.

    ```bash
    kubectl run --namespace=quickstart access --rm -ti --image busybox /bin/sh
    ```

    This command creates a BusyBox pod inside the `quickstart` namespace and starts a shell session inside the pod.

    ```bash title="Expected output"
    If you don't see a command prompt, try pressing enter.
    / #
    ```

5. In the BusyBox shell, run the following command to test communication with the NGINX server:

   ```bash
   wget -qO- http://nginx
   ```

   You should see the HTML content of the NGINX welcome page.

   ```html title="Expected output"
   <!DOCTYPE html>
   <html>
   <head>
   <title>Welcome to nginx!</title>
   <style>
   html { color-scheme: light dark; }
   body { width: 35em; margin: 0 auto;
   font-family: Tahoma, Verdana, Arial, sans-serif; }
   </style>
   </head>
   <body>
   <h1>Welcome to nginx!</h1>
   <p>If you see this page, the nginx web server is successfully installed and
   working. Further configuration is required.</p>

   <p>For online documentation and support please refer to
   <a href="http://nginx.org/">nginx.org</a>.<br/>
   Commercial support is available at
   <a href="http://nginx.com/">nginx.com</a>.</p>

   <p><em>Thank you for using nginx.</em></p>
   </body>
   </html>
   ```
   This confirms that the BusyBox pod can access the NGINX server.

6. In the Busybox shell, run the following command test communication with the public internet:

    ```bash
    wget -qO- https://docs.tigera.io/pod-connection-test.txt
    ```

    You should see the content of the file `pod-connectivity-test.txt`.

    ```html title="Expected output"
    You successfully connected to https://docs.tigera.io/pod-connection-test.txt.
    ```

    This confirms that the BusyBox pod can access the public internet.


7. Return to your browser to see the connection appear in the Whisker web console.
   You should see three new connection types: one to `coredns` one to `nginx`, and another to `PUBLIC NETWORK`.

   <Screenshot src="/images/whisker-quickstart-logs.png" alt="whisker2" />
   *Figure {figCount++}: Whisker web console showing allowed flows to NGINX server and `https://docs.tigera.io`.*

>You can filter the flow logs in Whisker using the dropdowns at the top.



[:arrow_right: Module 2 - Introducing Tiers](module-2-introducing-tiers.md)  

[:leftwards_arrow_with_hook: Back to Main](../README.md)  