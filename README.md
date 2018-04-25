
https://cloud.google.com/kubernetes-engine/docs/quickstart


gcloud container clusters create nd-edu

gcloud container clusters list

kubectl get services
NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.11.240.1   <none>        443/TCP   6m


https://github.com/kubernetes/kubernetes/issues/44377

https://github.com/mappedinn/kubernetes-nfs-volume-on-gke

gcloud compute disks create --size=10GB --type=pd-ssd gce-nfs-disk

$ gcloud compute disks create --size=10GB --type=pd-ssd gce-nfs-disk

    Created [https://www.googleapis.com/compute/v1/projects/nd-edu/zones/us-central1-a/disks/gce-nfs-disk].
    NAME          ZONE           SIZE_GB  TYPE    STATUS
    gce-nfs-disk  us-central1-a  10       pd-ssd  READY
    
    New disks are unformatted. You must format and mount a disk before it
    can be used. You can find instructions on how to do this at:
    
    https://cloud.google.com/compute/docs/disks/add-persistent-disk#formatting

Note - the format happens automatically for some reason in GCE :)

$ gcloud compute disks list

    NAME                                   ZONE           SIZE_GB  TYPE         STATUS
    gce-nfs-disk                           us-central1-a  10       pd-ssd       READY
    gke-nd-edu-default-pool-12578ca5-l8qt  us-central1-a  100      pd-standard  READY
    gke-nd-edu-default-pool-12578ca5-wstl  us-central1-a  100      pd-standard  READY

kubectl create -f 01-dep-nfs.yml 
kubectl describe deployment nfs-server
kubectl get pods

kubectl create -f 02-srv-nfs.yml 
kubectl create -f 03-pv-and-pvc-nfs.yml
kubectl create -f 04-dep-busybox.yml

kubectl exec -it nfs-busybox-7478d74df7-mlzxb -- busybox sh

kubectl exec -it nfs-server-7b6894fc6f-vjbmw -- /bin/bash

kubectl run my-shell --rm -i --tty --image ubuntu -- bash


