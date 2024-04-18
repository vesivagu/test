



```

[user01@server-1 openshift-april-2024]$ cat ~/openshift.txt
Red Hat OpenShift API Server Endpoint
+++++++++++++++++++++++++++++++++++++ 
https://api.ocp4.rpsconsulting.in:6443

Red Hat OpenShift web-console
+++++++++++++++++++++++++++++
https://console-openshift-console.apps.ocp4.rpsconsulting.in 

Login Credentials
+++++++++++++++++
user    : kubeadmin
password: mBMD4-fRIZo-BwPfQ-7quh7
-----------------------------

https://venkateshsivaguru.jfrog.io/artifactory/api/docker/venkatesh-docker

to login to jfrog art:
docker login -uvenkatesh89susila@gmail.com venkateshsivaguru.jfrog.io

password:
cmVmdGtuOjAxOjE3NDQ5NTYxNzg6Y1VwdmFyNGNrcDBaWFliZmN2MzQxVW9EMmtp

docker pull venkateshsivaguru.jfrog.io/venkatesh-docker/hello-world:latest


docker tag venkateshsivaguru.jfrog.io/venkatesh-docker/hello-world venkateshsivaguru.jfrog.io/venkatesh-docker/hello-world:1.0.0


docker push venkateshsivaguru.jfrog.io/venkatesh-docker/hello-world:1.0.0

-------------below are sample hello microservice-----------------

-- jrog enterprise - private openshift image registry

docker build -t tektutor/hello-microservice:1.0 .

docker tag tektutor/hello-microservice:1.0 venkateshsivaguru.jfrog.io/venkatesh-docker/hello-microservice:1.0.0

docker push venkateshsivaguru.jfrog.io/venkatesh-docker/hello-microservice:1.0.0

--update below in hello-microservice.deploy.yml
venkateshsivaguru.jfrog.io/venkatesh-docker/hello-microservice:1.0.0

oc create secret docker-registry private-jfrog-image-registry --docker-server=venkateshsivaguru.jfrog.io --docker-username=venkatesh89susila@gmail.com --docker-password=cmVmdGtuOjAxOjE3NDQ5NTYxNzg6Y1VwdmFyNGNrcDBaWFliZmN2MzQxVW9EMmtp

oc apply -f hello-microservice-deploy.yml

# oc new-app --image=venkateshsivaguru.jfrog.io/venkatesh-docker/hello-microservice:1.0



```
