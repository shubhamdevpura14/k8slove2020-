Task 1

create Dockerfile for httpd named "adhochttpd.dockerfile"

FROM centos
MAINTAINER shubhamdevpura@gmail.com
RUN yum install -y httpd
ENV x=app
EXPOSE 80
RUN mkdir /myapps
RUN mkdir /scripts
COPY beginner-html-site-styled /myapps/app1
COPY project-html-website /myapps/app2
COPY start.sh /scripts/start.sh
RUN chmod +x /scripts/start.sh
ENTRYPOINT ["/bin/bash","/scripts/start.sh"]

Git clone the webapps grom github and rename the folders

git clone https://github.com/mdn/beginner-html-site-styled
git clone https://github.com/microsoft/project-html-website

Make the script "start.sh"
#!/bin/bash

if [ "$x" == "app1" ]
then
        cp -rf /myapps/app1/* /var/www/html/
        httpd -DFOREGROUND

elif [ "$x" == "app2" ]
then
        cp -rf /myapps/app1/* /var/www/html/
        httpd -DFOREGROUND
else
        echo "You have not selected correct env for app1 or app2" > /var/www/html/index.html
        httpd -DFOREGROUND
fi
Docker build command
docker build -f adhochttpd.dockerfile -t shubhamdevpura/may2020q1:v1 .



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




Task 7

Run date command every 3 second and store output

Create pod file
apiVersion: v1
kind: Pod
metadata:
  labels:
    adhoc: shubhamdevpuraq7
  name: adhocpod7
spec:
  containers:
  - image: alpine
    name: adhocpod7
    command: ["/bin/shsh","-c","while true; do date>>/mnt/date.txt; sleep 3; done"]
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
Create pod file
kubectl create -f q7.yaml
