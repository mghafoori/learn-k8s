Tutorial for creating a test K8S cluster in Azure:

[6 Steps To Run .NET Core Apps In Azure Kubernetes](https://thorsten-hans.com/6-steps-to-run-netcore-apps-in-azure-kubernetes)

Note that it is a linux tutorial. There are some differences if you use PowerShell in Windows.

To store the ID of the Azure Container Registry (ACR) resource in a variable in PowerShell, use:

`$acr_id = az acr show -n nameOfAcr -g theResourceGroupName --query id -o tsv`

Use **--node-vm-size** option when creating the K8S cluster to change the VM type.  Default value is **Standard_DS2_v2**. But there are cheaper options like the **Standard_B2s**.

`az aks create -n nameOfCluster -g theResourceGroupName --enable-managed-identity --attach-acr $acr_id --node-count 1 --node-vm-size Standard_B2s`

Docker build and run:

`docker build -t milad.azurecr.io/web-app:1.0.0 .`

`docker run -p 8080:80 -it milad.azurecr.io/web-app:1.0.0`

kubectl tips:

`kubectl get pods --show-labels`

Test web-app:
curl http://localhost:8080/weatherforecast
curl http://{External IP}/weatherforecast