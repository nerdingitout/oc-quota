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
```
oc new-project quota-demo
```
## Configure a Pod Quota for a Namespace
- Create a ResourceQuota for the project that limits the number of pods to 2 using the following command
```
oc apply -f https://raw.githubusercontent.com/nerdingitout/oc-quota/main/project-quota.yaml
```
- Check if the ResourceQuota has been created successfully.
```
oc get resourcequota
```
![get resourcequota](https://user-images.githubusercontent.com/36239840/105810654-cba8d400-5fc4-11eb-9687-6b4b64f57192.JPG)
- You can also view the resource quota on the web console from the Administrator Perspective. Go to <b>Administration &#8594; Resource Quotas</b> as shown in the image below.
![resourcequota webconsole](https://user-images.githubusercontent.com/36239840/105811063-791be780-5fc5-11eb-8aa5-7950c7dc3b4a.JPG)
- If you view the details of the resource quota and scroll down to Resource Quota Details table, you can notice information on used and maximum resources. Since you haven't delpoyed any pods yet, it will show 0 pods used.
![quota details](https://user-images.githubusercontent.com/36239840/105811625-5b02b700-5fc6-11eb-8a95-06414df4b7d1.JPG)

## Verify that the Pod Quota works
- Deploy a simple application, we will scale it to 2 replicas in the next step
```
oc create deployment myguestbook --image=ibmcom/guestbook:v1 -n quota-demo
```
![image](https://user-images.githubusercontent.com/36239840/106387970-cc42cf80-63f5-11eb-8770-bec826f9a75e.png)
- If you use the the ```oc get pods``` command you will notice that the pod is in running state.
![image](https://user-images.githubusercontent.com/36239840/106388021-06ac6c80-63f6-11eb-9565-558f020633e2.png)
- If you go back to the Resource Quota 'pod-demo' on the web console, you will notice the number of used pods is now 1 as expected. This shows that the ResourceQuota has correctly accounted our Pod against the specified Quota
![image](https://user-images.githubusercontent.com/36239840/106388036-14fa8880-63f6-11eb-8c56-2411c358184d.png)
- Next, you will need to scale the application to 2 replicas. You can scale the application from both web console and command line. In this step, you will perform it from the web console. Go to <b>Workloads &#8594; Deployments</b> and click on 'myguestbook' deployment.
![deployments](https://user-images.githubusercontent.com/36239840/106388296-458ef200-63f7-11eb-8d7b-e0b354d7c2f0.JPG)
- Clicking on the upper arrow will increase number of replicas, down arrow decreases number of replicas. In this step you will need to increase number of replicas to 2.
![scale pods](https://user-images.githubusercontent.com/36239840/106388343-7bcc7180-63f7-11eb-9372-2c11b8ac2081.JPG)
- If you go back to the Resource Quota 'pod-demo' on the web console, you will notice the number of pods used has increased to 2.
![image](https://user-images.githubusercontent.com/36239840/106388411-d534a080-63f7-11eb-813f-515a2266fc20.png)
- Now, let's try exceeding the quota by adding another pod.
```
oc create deployment myguestbookv2 --image=ibmcom/guestbook:v2 -n quota-demo
```
![image](https://user-images.githubusercontent.com/36239840/106388658-06fa3700-63f9-11eb-8035-b1ff546b2868.png)
- If you run ```oc get pods``` you will notice that there are only 2 pods running even though you created a total of 3 pods.
![image](https://user-images.githubusercontent.com/36239840/106388687-2beeaa00-63f9-11eb-8518-0b487b8efde6.png)
- Go back to the web console and go to <b>Workloads &#8594; Deployments</b>. Notice the status of the pod showing '0 of 1 pods'
![deployments 2](https://user-images.githubusercontent.com/36239840/106388766-6ce6be80-63f9-11eb-9fc8-2ce9cb4a15d2.JPG)
- Click on the 'myguestbook2' deployment to view more details. You will notice that the pod hasn't been deployed.
![image](https://user-images.githubusercontent.com/36239840/106388869-db2b8100-63f9-11eb-82a4-b1a54011c9d9.png)
- If you scroll all the way down, you will notice the conditions section which shows that the pod has failed because the quota has been exceeded.
![failed pod](https://user-images.githubusercontent.com/36239840/106388947-2ba2de80-63fa-11eb-9b77-1c6db42271eb.JPG)

## Configure Memory and CPU for a Namespace
## Verify that the CPU and Memory Quotas work
## Summary
