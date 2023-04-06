## TASK 1: Setting up Authentication
- Configure cluster to use the HTPasswd identity provider
- Create the following user and groups
  - Group admins, with users admin and anna
  - Group developers, with users linda and developer
  - Group viewers, with user lisa
  - User anouk
- Ensure that all these users can log in to the cluster
- Remove the default kubeadmin user that was created when installing the cluster

### Solution:
1. htpasswd -c -b -B .htpasswd <USER> <PWD>
2. oc create secret generic htpasswd --from-file=htpasswd=.htpasswd -n openshift-config
3. oc adm groups new <GROUP>
4. oc adm groups add-users <GROUP> USER|[USERS]
5. oc edit oauth cluster
6. Test if able to log in
7. oc delete secret htpass-secret -n openshift-config
