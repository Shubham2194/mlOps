# mlOps

Official link for Kubeflow

https://www.kubeflow.org/docs/components/pipelines/legacy-v1/introduction/

Step 1 :
Run kubernetes cluster (EKS , Kind , minikube etc)
i am using kind here , Installing Kind


```
# For Intel Macs:


[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-darwin-amd64
# For M1 / ARM Macs
[ $(uname -m) = arm64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-darwin-arm64
chmod +x ./kind
mv ./kind /some-dir-in-your-PATH/kind
```

```

# For AMD64 / x86_64 [Linux]:

[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

```
#On Windows in PowerShell:


curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.29.0/kind-windows-amd64
Move-Item .\kind-windows-amd64.exe c:\some-dir-in-your-PATH\kind.exe

```

<img width="1256" alt="image" src="https://github.com/user-attachments/assets/ee48cadc-e432-4d0f-93a7-6aca2c8475a0" />


Step 2:
Run kind Cluster

```
kind create cluster --name kubeflow

```

(Note: Before runnig it make sure you Docker is up and running)

<img width="844" alt="image" src="https://github.com/user-attachments/assets/6f0a9baf-4ef8-4403-afef-1a50dc52c73d" />

Step 3:
Check cluster is running 

```
kubectl get pods -A
kubectl get nodes,ns
```

<img width="1090" alt="image" src="https://github.com/user-attachments/assets/dd2c7907-1354-4796-91b5-4ae801f40434" />

If you have cluster running already please switch to kind cluster using:
```
kubectl config get-contexts
kubectl config use-context kind-kubeflow (change name according to you cluster name)
```

Step 4:
Deploying Kubeflow Pipelines
The installation process for Kubeflow Pipelines is the same for all three environments covered in this guide: kind, K3s, Docker-desktop, and K3ai.

To deploy the Kubeflow Pipelines, run the following commands:

```
export PIPELINE_VERSION=2.4.0
kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-scoped-resources?ref=$PIPELINE_VERSION"
kubectl wait --for condition=established --timeout=60s crd/applications.app.k8s.io
kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic?ref=$PIPELINE_VERSION"
```

<img width="1391" alt="image" src="https://github.com/user-attachments/assets/1a5ea074-52c6-43f9-bafd-90b723653804" />


Step 5:
This will create new namespace as kubeflow and run all the required pods.

```
kubectl get pods -n kubeflow
```


<img width="1148" alt="image" src="https://github.com/user-attachments/assets/c2c7c97b-3002-4d2a-8849-4e2f6c74b541" />

Step 6:
After some wait everything is up and running

<img width="991" alt="image" src="https://github.com/user-attachments/assets/bd044210-7216-4a5a-8ca1-b6ceb264b805" />


Step 7:
Verify that the Kubeflow Pipelines UI is accessible by port-forwarding:

```
kubectl port-forward -n kubeflow svc/ml-pipeline-ui 8080:80
```

<img width="982" alt="image" src="https://github.com/user-attachments/assets/beb87283-6623-48d7-af97-d5c43a63ec2e" />


<img width="1630" alt="image" src="https://github.com/user-attachments/assets/8cd46f6a-9677-49cc-a2e4-cb97168bf791" />


So we have deployed Kubeflow pipeline  successfully on kind cluster

Step 8 :



















