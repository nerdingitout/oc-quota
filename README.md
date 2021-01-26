# Enforcing resource consumption limits using OpenShift ResourceQuota
## Introduction
When several users or teams share a cluster with a fixed number of nodes, there is a concern that one team could use more than its fair share of resources. Therefore, resource quota is a tool for administrators to address this concern.<br>
A resource quota provides constraints that limit aggregate resource consumption per project or pod/container. It can limit the quantity of objects that can be created in a project by type, as well as the total amount of compute and storage resources that may be consumed by resources in that project.<br>
In Red Hat OpenShift, you can manage constraints on a project level using the Resource Quota object or on a pod/container level using the Limit Range object.<br>
In Limit Ranges, you can specify the minimum and maximum usage of memory and CPU. As for Resource Quotas, you can specify amount of memory and CPU and number of Pods, replication controllers, services, secrets and presistent volume claims.<br>
A resource quota is enforced on a project or pod/container when there is ResourceQuota/LimitRange specified.

## Prerequisites
For this tutorial you will need:
- Red Hat OpenShift Cluster 4.3 on IBM Cloud.
- oc CLI (can be downloaded from this link or you can use it at http://shell.cloud.ibm.com/.
## Estimated Time
It will take you around 30 minutes to complete this tutorial.
## Steps
- Create a Project & Enforce Resource Quota
- Configure a Pod Quota for a Namespace
- Verify that the Pod Quota works
- Configure Memory and CPU for a Namespace
- Verify that the CPU and Memory Quotas work

## Login to the CLI & Create a Project
- Go to the web console and click on your username at the top right then 'Copy Login Command', then display the token and copy the ```oc login``` command in your terminal.<br>
![login](https://user-images.githubusercontent.com/36239840/97104809-26821500-16d0-11eb-936e-c2b7fb914523.JPG)
- From the CLI, create a project and name it 'quota-demo' as shown in the following command.<br>
```oc new-project quota-demo```
## Enforce a ResourceQuota
- Create a ResourceQuota for the project that limits the number of pods to 2 using the following command
```oc apply -f https://raw.githubusercontent.com/nerdingitout/oc-quota/main/project-quota.yaml```
- Check if the ResourceQuota has been created successfully.
```oc get resourcequota```
![get resourcequota](https://user-images.githubusercontent.com/36239840/105810654-cba8d400-5fc4-11eb-9687-6b4b64f57192.JPG)
- You can also view the resource quota on the web console from the Administrator Perspective. Go to <b>Administration &#8594; Resource Quotas</b> as shown in the image below.
![resourcequota webconsole](https://user-images.githubusercontent.com/36239840/105811063-791be780-5fc5-11eb-8aa5-7950c7dc3b4a.JPG)
- If you view the details of the resource quota and scroll down to Resource Quota Details table, you can notice information on used and maximum resources. Since you haven't delpoyed any pods yet, it will show 0 pods used.
![quota details](https://user-images.githubusercontent.com/36239840/105811625-5b02b700-5fc6-11eb-8a95-06414df4b7d1.JPG)


## Configure a Pod Quota for a Namespace
## Verify that the Pod Quota works
## Configure Memory and CPU for a Namespace
## Verify that the CPU and Memory Quotas work
## Summary
