
# flavour-E-Docs
Follow the steps in this wiki to setup Rancher in AWS and to deploy icap, squip and nginx pods
https://k8-proxy.github.io/k8-proxy-documentation/docs/flavors/flavor-a/manual-setup-aws#setting-up-aws-ec2-instance-for-rancher-for-flavour-a


## Setting up ICAP Infrastructure
1.  Clone the https://github.com/k8-proxy/icap-infrastructure repository
    ```
        git clone https://github.com/k8-proxy/icap-infrastructure.git
    ```
    then run the following commands
    ```
    cd icap-infrastructure/adaptation
    kubectl create ns icap-adaptation
    kubectl create -n icap-adaptation secret generic transactionstoresecret --from-literal=accountName=guest --from-literal=accountKey=guest
    ```
    ####Edit the event-submission-deployment.yml and change transactionStoreSecret to transactionstoresecret(Only required for the time I am cloning this branch i.e commit id 539a0ed4da97c445bcfa27e8fa5185ccb2494d8e)

2. Follow the doc https://github.com/k8-proxy/icap-infrastructure#adaptation-cluster until the **helm install** command
3. Run the command
   ```
   kubectl get configmap/tcp-services -ningress-nginx -o yaml > tcp_services_icap3.yaml
   ```
4. Edit the yaml file
   ```
     vim tcp_services_icap3.yaml
   ```
   and add the following at the end of the fil
   ```
   data:
    "1344": icap-adaptation/icap-service:1344
   ```
5. Install c-icap
   ```
    sudo apt-get install c-icap
   ```
6. Run the command but replace the Elastic IP text
   ```
     c-icap -i <Elastic IP>
   ```

