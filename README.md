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