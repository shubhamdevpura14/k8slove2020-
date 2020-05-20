Task 2
write a pod file and host it k8s

Create pod file named "q2.yaml" 

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    adhoc: rhythmbhiwaniq2
  name: adhocpod1
spec:
  containers:
  - image: nginx
    name: adhocpod1
    ports:
    - containerPort: 80
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

Create the pod

kubectl create -f q2.yaml
Create file for service named "q2srvrhythmbhiwani.yaml"
apiVersion: v1
kind: Service
metadata:
  name: q2srvrhythmbhiwani
spec:
  type: NodePort
  selector:
    adhoc: rhythmbhiwaniq2
  ports:
    - port: 80
      targetPort: 80
      
Create the service

kubectl create -f q2svcrhythmbhiwani.yaml
