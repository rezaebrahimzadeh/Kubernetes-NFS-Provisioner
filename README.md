To set up a Kubernetes NFS provisioner, you can follow a process that involves creating an NFS server, configuring your Kubernetes cluster to recognize and use this server for dynamic provisioning, and then deploying an NFS client provisioner within your cluster. Here's a step-by-step guide based on the provided sources

Prerequisites: 
To set up a Kubernetes NFS Provisioner using Mnifests yaml files, you can follow these steps,
Ensure NFS Server Accessibility: Make sure your NFS server is accessible from your Kubernetes cluster. You need the NFS server's hostname and the exported share path.
Create a Namespace: Create a namespace for your NFS provisioner. For example, you can name it nfs-provisioner

Start:

- git clone https://github.com/rezaebrahimzadeh/Kubernetes-NFS-Provisioner.git

Create a Namespace: Create a namespace for your NFS provisioner. For example, you can name it nfs-provisioner

- kubelctl apply -f namespace.yml

We need to create the necessary accesses for the NFS service, which we do using rbac.yml

- kubectl apply -f rbac.yml

Note: Make sure it is created use >> kubectl get roles,After you are sure it has been created apply in StorageClass.yml

Note:  whatever name you choose for the provisioner must match the PROVISIONER_NAME deployment env
Note: when set archiveOnDelete in "flase" >> If we delete the PVC, our data will be deleted from the NFS 
Note: when set archiveOnDelete in "true"  >> If we remove PVC, our data will remain in NFS
Default set in false 


- kubectl apply -f StorageClass.yml

After apply StorageClass.yml use in command for check 
- kubectl get sc 


Now apply storage class deplyment 

Note: please Replace env NFS_SERVER and NFS_PATH Your nfs server details.


- kubectl apply -f storage-class-deployment.yml


now check pod is running 

- kubectl get po -n nfs-provisioner

For testing, you can create a PVC using a "pvc-claim-test.yml" and also create a deployment "deployment-test.yml" that uses the same test PVC and check that its data is placed in the NFS server.

Note: This package must be installed on Kubernetes worker nodes
- sudo apt install nfs-common
