## Upgrade helm step by step

1. IF your helm chart use StatefulSet with VolumePersistentClaim
- Delete your StatefulSet with parameter `--cascade` 
- Upgrade with helm command `helm upgrade -f value.yaml mongodb stable/mongodb-replicaset`

2. IF no StatefulSet with VolumePersistentClaim

- Upgrade by helm command
