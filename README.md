# Pre-requisites
- Get Azure Pass from https://aka.ms/JBHackMay2024
![image](https://github.com/san360/hackathon/assets/6613457/e2c19945-b1b3-4394-9079-37bb92252f89)
- Existing account or new account may be required for getting azure subscription

# AKS Cluster setup
### Create Resource Group
```
az group create -l NorthEurope -n jb-k8s-hackathon-rg
```

### Deploy template with in-line parameters
```
az deployment group create -g jb-k8s-hackathon-rg  --template-uri https://github.com/Azure/AKS-Construction/releases/download/0.10.5/main.json --parameters \
	resourceName=jb-k8s-hackathon \
	agentCount=1 \
	JustUseSystemPool=true \
	registries_sku=Basic \
	acrPushRolePrincipalId=$(az ad signed-in-user show --query id --out tsv) \
	enableTelemetry=false \
	omsagent=true \
	retentionInDays=30 \
	fileCSIDriver=false \
	diskCSIDriver=false
```
### Get credentials for your new AKS cluster & login (interactive)
```
az aks get-credentials -g jb-k8s-hackathon-rg -n aks-jb-k8s-hackathon
```
### Get nodes from kubernetes
```
kubectl get nodes
```
![image](https://github.com/san360/hackathon/assets/6613457/c6dcf740-3593-4723-9c82-6eec268730b3)
