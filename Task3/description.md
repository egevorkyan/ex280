## Task 3: Creating a Project Template
- Create a new project template, according to the following requirements
  - Each project has a label with the name of the project
  - Network Policy is set up such that:
    - Routes can be accessed by Pods in namespaces with the network.openshift.io/policy-group=ingress label
    - Pods in the same namespace can communicate with each other
    - Pods are only accessible to Pods in a different namespace if that namespace is configured with the network.openshift.io/policy-group=ingress label
  - Limit range is set up as follows:
    - Each container requests 100 milli-cores of CPU
    - Each container requests 50 MiB of memory
    - Each container is limited to 200 milli-cores of CPU
    - Each container is limited to 100 MiB of memory
  - Resource Quota is set up as follows:
    - Projects are limited to 20 Pods
    - Project can request a maximum of 1 GiB of memory
    - Projects can request a maximum of 2 CPUs
    - Projects can use a maximum of 2 GiB of memory
    - Projects can use a maximum of 4 CPUs
### Solution:
1. oc adm create-bootstrap-project-template -o yaml > project-template.yaml
2. add labels section in metadata
   labels:
     name: ${PROJECT_NAME}
3. use limit range official documentation to do not memorize syntax
4. use quota official documentation to do not memorize syntax
5. use network policy official documentation to do not memorize syntax
6. oc create -f project-template.yaml -n openshift-config
7. To check: oc get pods -n openshift-apiserver
8. Check if applied
   - oc new-project demo
   - oc describe project demo