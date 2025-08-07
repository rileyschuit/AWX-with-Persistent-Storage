Summary:  This is an example adding on to an install of AWX.  This will assist with persisting storage on NFS if something really bad was to happen. 

Requirements:
1.  Functional NFS server

Steps:

Adjust sample files as needed.  

1. Optional: Needs new namespace
2. Optional after you create your namespace:
```
change default namespace:  'kubectl config set-context --current --namespace=awx'
```
 
Apply using kubectl:
'kubectl apply -k .'

You can watch the progress of awx install with command:
``` 
'kubectl logs -f deployments/awx-operator-controller-manager -c awx-manager'
```

To get the newly generated admin password, run this:
```
kubectl get secret awx-admin-password -n awx -o jsonpath="{.data.password}" | base64 --decode
```

Testing details:  
*  Set this up with 2.19.0, changed the admin password, make an example org
*  Adjusted kustomization.yml for 2.19.1 to check if the migration worked as it should, BUG:  IT DOESN'T
*  Logged in to test BUG:  IT DOESN'T

TODOs:
* Need to read the docs on backups and/or migration

Other documents you can look at:
[Basic Install](https://ansible.readthedocs.io/projects/awx-operator/en/latest/installation/basic-install.html)
[Database Configurations](https://ansible.readthedocs.io/projects/awx-operator/en/latest/user-guide/database-configuration.html)
[Kubernetes NFS Subdir External Provisioner](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner)