# Create GPU node pool

- Create GKE cluster 1 zone (check resource for region and zone with GPU supported)

```
gcloud container clusters create [CLUSTER_NAME] --zone [ZONE_WITH_GPU_SUPPORT] --num-nodes 1
```

- Create GPU node pool in this GKE cluster

```
gcloud container node-pools create ${GPU_POOL_NAME} \                                                                                                   
                --accelerator type=nvidia-tesla-p4,count=1 \
                --zone asia-southeast1-b --cluster vision-gke \    
                --num-nodes=1 --machine-type=n1-standard-4 --min-nodes=0 --max-nodes=1 --enable-autoscaling

```

#### Official NVIDIA GPU device plugin
 
To deploy the NVIDIA device plugin once your cluster is running and the above requirements are satisfied:

```
kubectl create -f https://raw.githubusercontent.com/NVIDIA/k8s-device-plugin/1.0.0-beta/nvidia-device-plugin.yml
```

#### NVIDIA GPU device plugin used by GCE

The NVIDIA GPU device plugin used by GCE doesn’t require using nvidia-docker and should work with any container runtime that is compatible with the Kubernetes Container Runtime Interface (CRI). It’s tested on Container-Optimized OS and has experimental code for Ubuntu from 1.9 onwards.

You can use the following commands to install the NVIDIA drivers and device plugin:

```
# Install NVIDIA drivers on Container-Optimized OS:
kubectl create -f https://raw.githubusercontent.com/GoogleCloudPlatform/container-engine-accelerators/stable/daemonset.yaml

# Install NVIDIA drivers on Ubuntu (experimental):
kubectl create -f https://raw.githubusercontent.com/GoogleCloudPlatform/container-engine-accelerators/stable/nvidia-driver-installer/ubuntu/daemonset.yaml

# Install the device plugin:
kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/release-1.14/cluster/addons/device-plugins/nvidia-gpu/daemonset.yaml
```