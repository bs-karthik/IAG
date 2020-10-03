# Openshift Commands

### Openshift cluster start 
`oc cluster up --base-dir ~/openshift.local.clusterup`

### Openshift cluster down 
`oc cluster down`
### Create new project as developer 
`oc new-project project1`

### Customize the template file available from product as per your needs and upload
`oc create -f kbs/openshift/project1/default-template.yaml`

### Create configmap, make sure the name matches the default value in the template or supply as parameter during the new-app 
For this example , i am creating the configmap name to match the default value in the template 
Create specific file during the configmap, else the container will fail to start 

`oc create configmap iag-config --from-file=${PWD}/kbs/openshift/project1/files/config.yaml`
### Create secret for all the keystores 
`oc create secret generic iag-secret --from-file=${PWD}/kbs/openshift/project1/files/secret_files1`

### Create new-application using the template file, supply the value of the application explictly 
`oc new-app --template=ibm-app-gateway -p APP_NAME=app1`

### Get logs 
`oc logs -f deploy/app1`

## Delete all Resources, delete in order and recreate above steps 
```
oc delete all -l app=app1
oc delete configmap iag-config
oc delete secret iag-secret
oc delete template ibm-app-gateway
#oc delete project project1
```

### After any changes to re-deploy 
`oc get deploy app1 -o yaml | oc apply -f -`
