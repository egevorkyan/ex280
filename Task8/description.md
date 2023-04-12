## Task 8: Configure MySQL
- As the developer user, use a deployment to create an application named mysql in the microservice project
- Create a generic secret named mysql, using password as the key and mypassword as its value. Use this secret to set the
  MYSQL_ROOT_PASSWORD environment variable to the value of the password in the secret.
- Configure the MySQL application to mount a PVC to /mnt. The PVC must have a 1GiB size, and the ReadWriteOnce access mode
- Use a Nodeselector to ensure that MySQL will only run on your CRC node
### Solution:
1. oc new-project microservice
2. oc create secret generic mysql --from-literal password=mypassword
3. oc new-app --name mysql --image mysql
4. oc set env deploy mysql --prefix MYSQL_ROOT_ --from secret/mysql
5. oc set volumes deploy mysql --name mysql-pvc --add -m /mnt --claim-size='1Gi' --claim-name='mysql-pvc' --claim-mode='ReadWriteOnce'
6. oc login -u <ADMINISTRATIVE_USER>
7. oc get nodes
8. oc label nodes crc-9vl9r-master-0 role=master
9. oc login -u developer
10. oc edit deploy mysql
    - Add below lines under spec section
      ```yaml
      nodeSelector:
        role: master
      ```