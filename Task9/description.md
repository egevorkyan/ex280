## Task 8: Configure WordPress
- As the developer user, use a deployment to create an application named WordPress in the microservice project
- Run this application with the anyuid security context assigned to the wordpress-sa service account
- Create a route to the WordPress application, using the hostname wordpress-microservice.apps-crc.testing
- Use secrets and or ConfigMaps to set environment variables:
  - WORDPRESS_DB_HOST: is set to mysql
  - WORDPRESS_DB_NAME: is set to value of wordpress 
  - WORDPRESS_DB_USER: has the value "root"
  - WORDPRESS_DB_PASSWORD: is set to the value of the password key in the mysql secret
### Solution:
1. oc new-app --name wordpress --image wordpress
2. oc create configmap wordpress --from-literal host=mysql --from-literal name=wordpress --from-literal user=root
3. oc set env deploy wordpress --prefix=WORDPRESS_DB_ --from cm/wordpress
4. oc set env deploy wordpress --prefix=WORDPRESS_DB_ --from secret/mysql
5. oc create sa wordpress-sa
6. oc login -u <ADMINISTRATIVE_USER>
7. oc adm policy add-scc-to-user anyuid -z wordpress-sa
8. oc login -u developer
9. oc set serviceaccount deployment wordpress wordpress-sa
10. oc expose service wordpress --hostname wordpress-microservice.apps-crc.testing