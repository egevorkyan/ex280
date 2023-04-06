## Task 2: Setting up Authorization
- The group admins has admin permissions on the cluster
- The group developers has view and edit permissions on the cluster
- The group viewers has view permissions on the cluster
- User anouk has view and edit permissions on the namespace test-namespace

### Solution:
1. oc adm policy add-cluster-role-to-group <ROLE> <GROUP>
2. oc adm policy add-role-to-user <ROLE> <USER> -n <NAMESPACE>