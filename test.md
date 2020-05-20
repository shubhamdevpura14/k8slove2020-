Task 2
write a pod file and host it k8s

Create pod file named "q2.yaml" 

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    adhoc: shubhamdevpuraq2
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
Create file for service named "q2srvshubhamdevpura.yaml"
apiVersion: v1
kind: Service
metadata:
  name: q2srvshubhamdevpura
spec:
  type: NodePort
  selector:
    adhoc: shubhamdevpuraq2
  ports:
    - port: 80
      targetPort: 80
      
Create the service

kubectl create -f q2svcshubhamdevpura.yaml





Task 5

deployment create

Create file named "q1dep1.yaml"

apiVersion: apps/v1
kind: Deployment
metadata:
  name: adhhocdeprhythmbhiwani5
  labels:
    adhoc: rhythmbhiwaniq5
spec:
  replicas: 3
  selector:
    matchLabels:
      adhoc: rhythmbhiwaniq5
  template:
    metadata:
      labels:
        adhoc: rhythmbhiwaniq5
    spec:
       containers:
        - env:
          - name: x
            value: app2
          image: rhythmbhiwani/may2020q1:v1
          imagePullPolicy: Always
          name: adhocpod2
          ports:
          - containerPort: 80
          
Create the deployment

kubectl create -f q5dep1.yaml

Create service file named "q5svcrhythmbhiwani.yaml"

apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    adhoc: q5svcrhythmbhiwani
  name: q5svcrhythmbhiwani
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    adhoc: rhythmbhiwaniq5
  type: LoadBalancer
  
Create the service

kubectl create -f q5svcrhythmbhiwani.yaml
