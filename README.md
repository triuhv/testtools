### Base image for triuhv/testtools
- debian os
- ssh
- curl
- rclone  
  
 **Using it on Docker environment :**  
`docker run -it --name testtools triuhv/testtools:v1.0 /bin/sh -c "while true; do echo 'busybox running'; sleep 10;done"`
  
`docker exec -it testtools bash`  
  
root@2be2625c49a7:/# ping google.com  

**Using it on Kubernetes environment :**  
1.  Create new testtools.yaml  
apiVersion: v1  
kind: Pod  
metadata:  
  name: testtools  
  labels:  
    app: testtools  
spec:  
  containers:  
  \- name: testtools  
    image: triuhv/testtools:v1.0  
    resources: {}  
    command: ["/bin/bash"]  
    args: ["-c", "while true; do echo 'busybox running'; sleep 10;done"]  
2. Run apply pod  
`kubectl apply -f testtools.yaml  
3. Access to pob  
`kubectl exec -it pod/testtools bash  
  
   root@2be2625c49a7:/# ping google.com   
  
**Using it on OpenShift 3.11 environment :**  
`oc login  
Username: developer  
Password:  
  
`oc project myproject  
`oc new-app --docker-image=triuhv/testtools:v1.0 -l method=testtools    
  
Node: Update deployment yaml by  
      \- command:  
          \- /bin/sh  
          \- '-c'  
          \- while true; do echo 'busybox running'; sleep 10;done  
 
