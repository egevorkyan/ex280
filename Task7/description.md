## Task 7: Configure AutoScaling
- Run a deployment that starts the bitnami nginx service. Create it to run three pods by default,
  and scale to a max of five pods if the CPU utilization exceeds 70%
### Solution:
1. oc create deployment bnginx --image bitnami/nginx:latest --replicas=3
2. oc autoscale deployment bnginx --min 1 --max 5 --cpu-percent=70