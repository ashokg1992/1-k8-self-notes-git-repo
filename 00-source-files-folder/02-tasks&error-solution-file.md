---
# good source for errors
01- https://x.com/techyoutbe/status/1816924469681881578   34 Potential Issues in a Multi-Cluster Kubernetes Environment (with Error Message )

02- 


#########  Real time Case Scenario and Troubleshooting in Kubernetes Production Environment  ############

Not able to deploy application getting error Resource mapping not found - Part -01 - https://youtu.be/Sa-zKp9vytk

Not able to deploy application getting error Resource mapping not found - Part -03 - https://youtu.be/XnPAY85TWM8

Not able to deploy application getting error Resource mapping not found - Part -02 - https://youtu.be/N5hHVd_4hrc

-----

Application Pod Created but not Found in Cluster - Part -01             -   https://youtu.be/dlNfruLuo4Q

Application Pod Created but not Found in Cluster - Part -01             -    https://youtu.be/25B2GLc5uBo

How to deploy application on Kubernetes using CICD Pipeline | Part -01  -    https://youtu.be/Cf8s5g5a1PY

How to deploy application on Kubernetes using CICD Pipeline | Part -02  -    https://youtu.be/RI-4_JMUhJE


How do we setup Pod down alert on Kubernetes cluster … 

it’s very hard to monitor all cluster in project because generally we managed 100+ kubernetes cluster so  that if any pod down then we will get email notification then we can connect to that cluster and fix the issue


Pod down Alert on email Notification  | Alert setup on Kubernetes | Troubleshooting
https://youtu.be/QxhLpOVjPd0

Generally if pod restarted then new Pod come up then we can’t check old pod related logs to get RCA for this so we can use EFK to store logs of failed pod

How to check Failed POD logs in KIBANA dashboard | Elastic search Fleuntd and KIBANA |EFK Kubernetes
https://youtu.be/5Uuqd8UilIg

===========
The "OOMKilled" error indicates that your pod has been terminated by the Kubernetes system because it exceeded its memory limit. This issue can be addressed by following these steps:

1. Check Current Memory Usage and Limits
First, identify the current memory usage and limits for the pod.

sh
Copy code
kubectl describe pod <pod-name> -n <namespace>
Look for the Resources section, which details the limits and requests for memory.

2. Increase Memory Limits
If your pod consistently exceeds its memory limit, you need to increase the limit. This can be done by editing the deployment configuration or the pod spec.

yaml
Copy code
resources:
  requests:
    memory: "512Mi"
  limits:
    memory: "1Gi"
Update the values according to your needs. You can edit your deployment configuration using:

sh
Copy code
kubectl edit deployment <deployment-name> -n <namespace>
Or by updating the YAML file and applying it:

sh
Copy code
kubectl apply -f <deployment-file>.yaml
3. Optimize Application Memory Usage
Sometimes, increasing the memory limits isn't the best long-term solution. Investigate and optimize the memory usage of your application:

Memory Leaks: Ensure there are no memory leaks in your application.
Efficient Algorithms: Optimize your algorithms to use less memory.
Load Testing: Perform load testing to understand memory usage under different loads.
4. Monitor Memory Usage
Set up monitoring for your pods to track memory usage over time. Tools like Prometheus, Grafana, and the Kubernetes Dashboard can help with this.

5. Configure Eviction Policies
Kubernetes has eviction policies that can be configured to prevent OOMKilled errors. You can set thresholds to evict pods when they exceed certain resource limits.

Example of Configuring Resource Limits
Here's an example of how to configure resource limits in a pod spec:

yaml
Copy code
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
  - name: example-container
    image: example-image
    resources:
      requests:
        memory: "512Mi"
      limits:
        memory: "1Gi"
6. Investigate Node-Level Issues
Ensure that the node running your pod has enough memory. Sometimes, node-level issues can cause pods to be OOMKilled. Check node memory usage with:

sh
Copy code
kubectl describe node <node-name>
7. Horizontal Pod Autoscaling
If the high memory usage is due to increased load, consider using Horizontal Pod Autoscaling (HPA) to automatically scale the number of pod replicas.

sh
Copy code
kubectl autoscale deployment <deployment-name> --cpu-percent=50 --min=1 --max=10
This command will scale the deployment based on CPU usage, but you can adjust it to consider memory usage as well by configuring custom metrics.

Summary
Identify current memory usage and limits using kubectl describe pod.
Increase memory limits if necessary by editing the deployment configuration.
Optimize application memory usage to prevent excessive memory consumption.
Monitor memory usage over time using tools like Prometheus and Grafana.
Configure eviction policies to manage resource limits effectively.
Investigate node-level issues to ensure nodes have adequate resources.
Consider horizontal pod autoscaling to handle increased load dynamically.
By following these steps, you can address the OOMKilled error and ensure your pods have the necessary resources to function correctly.


===========erors 

- pvc stuck in terminstaing state
-pod getting image pull backoff error due to authorization 
-application url is down 
- how do you extend persistent volume
-not able to connect cluster from jump server
- pods are in failed state
- application pod is stuck due to zone mismatch
- cluste is unstable after upgradation  
- we have one deployment file,having two replicas, I want both pods running on two different nodes,  

   ans ) generally give answer like that we can apply node selector but this is wrong answer because if you apply node selector at deployment level so all pods should be running over the same node but here question is I want all
Pods needs to be running in different different node.. this is very common case scenario customer want to do it

-In Kubernetes, pod-to-pod communication is important.

In one of the previous post I said that the most common issues are around: 

1. The CNI.
2. Firewall.

Here are 5 more:

3. Anti-affinity rules.
4. DNS resolution issues.
5. Messed up network policies.
6. Misconfigured service settings.
7. Faulty network hardware on worker nodes.

Why should you know this?

Because knowing these will help you quickly troubleshoot your Kubernetes problems.

-what is the difference between Config-Map & Secrets file in K8S ?

Config-Map :

Config-Map  is used to externalize configuration properties in the application. This means instead of hard-coding the configuration properties(data-source component) we will define those in the Config-Map.yml file. Config-Map stores the non-sensitive data

Secrets:
                Secrets file stores the sensitive data.  In Secrets files before the data is going to store in secrets file the data is encrypted at rest so that hackers cannot read the data & no key/access to decrypt the data. For Secrets file we even can have least privileges by using RBAC.

-Nginx Ingress controller Upgrdation and Monitoring using grafana and prometheus setup

End to end implementation of Grafana and Prometheus from scratch level on Kubernetes and created multiple grafana dashboard for monitoring 

- How do we Migrate Kubernetes Resources from One cluster to another Cluster or from one region to another region
- I have 10 nmaespaces available, we found 3 namespaces consume 80% resources of worker node, how do overcome this issue wothoiut increase resourcs of worker node
- customer want the solution that when application team deploy new patches or update on application pod, during the upation time our application should be availbble , how we can achiheve this one 
- UNABLE TO CREATE RESOURCE ON CLUSTER,
ans) after troubleshooting found that quota limit full on namespace level

# this is case on production namespacelevel in k8
- max pod created up tp 20 on namespace
-all pod consumption max up to 200 gb
-all pod consumption max up to 16 cpu
-limits total storage requesteddddd to 500Gi
-limits the number of pvc to 5
these are the requirement from Customer to apply of namespace

# After Application Upgradation ..my application down ..how do we Roll back to previous Version of POD

# I got one incident that one of my Application Volume size Crossed Threshold up to 90% Volume size Full Due to this Pod having Crash Loopback Off Error.
In My Application POD having 200GB and Out 200GB-180GB Has been Utilized So In that Case How Do we Increased Size of PVC on Existing Application.

# I got one incident that one of my Application Volume size Crossed Threshold upto 90% Volume size Full Due to this Pod having Crash Loopback Off Error. To Fix This Issue I need to be Login Inside Container and Cleared Old Logs file, tmp File, WAR file But unable to do Due to Pod Down and Customer Don't want allow to Increase size of PVC. Then how to Fix this Issue.

# I got one incident that one of my Application POD has been Stuck in Pending State, So How do we Check Events or Logs Of Application and What are the Root Cause of the Issue. how do we Fixed This type of Issue

# I got one incident that one of my Application POD has been Crashed and it Restarted Frequently but after several way of troubleshooting It does not Fix Then After I have to check with Application team, they want only data which one Inside failed Pod so that they have to use in other Pod So In this How we can Restore Data on failed POD


#What is Velero backup Tool, why we use

How do we setup velero plugins to jump server

How do we create service principle in azure

How to we create bucket in Azure to store backup data

How do we Autheticate backup tool with Azure Kubernetes Cluster

How do we setup Velero server as a pod on Kubernetes Cluster

How do we take full back up on entire namespace

How do we restore namespace from backup After deletion

How do we set Retention period during backup command

How we set schedule backup in KubernetesHow do we delete backup and restore

How do we cross verify that how many total resources has been backed.

# 
1 - How do we Plan for Kubernetes Cluster Upgradation
2- What are Pre and Post Task During Kubernetes Cluster Upgradation
3- How do we get Information about to Which Version I have to Update First ➡ 4 - What are Common Case Failure for Cluster upgradation and How do we Fix those Issue
5- How do We Check My existing Application is Compatible With Latest Version of Kubernetes Cluster
6- How do We Check Compatibility Matrix with upgraded Kubernetes Version like (Velero, Nginx Ingress Controller, Rancher etc)
I Have Covered two Failure Case Scenario and Provided RCA and Solution during Cluster upgradation


# which Version you have Upgraded and how do we check compatibility matrix with Latest version of kubernetes and what type of challenges you faced during Cluster Upgradation and how do you fix those issue

# can not evict pod due restrictive pod diisturption budjet policy, how you fix it
# My Backup is getting Failed …. Unable to take Backup , how do you do this ?
# 
Which Services Mostly Uses in Kubernetes Production Env
How Traffic Flow from Inside Pod to outside Network
➡Where we have Define URL of Application so that I Can access. my Application Using URL (www. http://webapprouting.kubernetes.azure.com/ )
How do We Make Sure Your Application Running over HTTPS
How do We Generate SSL or TLS Certificate
How do we Import TLS Certificate in Application

# HOW DO WE UPGRADE APP AFTER KUBERNETES CLUSTER UPGRDATION, HOW DO WE CHECK APPLICATION COMPATIBILITY MATRIX AFTER CLUSTER UPGRDATION
# 
Project -How do we install Jenkins as pod through Helm Chart
How to Download Values.yaml file form Helm Chart
I want to do some customization on values.yaml
I want to use private repo in image registry for Jenkins pod in
How do we RollBack to Previous Version using Helm

# ONE OF APPLICATION URL NOT WORKING, WHAT ARE THE root cause analysis FOR THIS HOW DO WE FIX THOSE ISSUE ,IF URL DOWN FIRST THINGS WHAT I HAVE TO CHECK I HAVE CREATED CHECKLIST WHIHC YOU HAVE TO FOLLOW  

# 








-