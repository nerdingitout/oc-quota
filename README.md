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

## Create a Project & Enforce Resource Quota
## Configure a Pod Quota for a Namespace
## Verify that the Pod Quota works
## Configure Memory and CPU for a Namespace
## Verify that the CPU and Memory Quotas work
## Summary
