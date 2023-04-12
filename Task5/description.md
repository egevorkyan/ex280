## Task 5: Running a Secure Application
- Create the project my-project
- In this project, run a deployment that is based on the Docker image eduard1001171985/hello-world-secure:1.0 with the name hello-app
- Configure this deployment such that it uses a TLS certificate at the expected location. Use the TLS certificate that was created in the preparation steps of this lab

### Solution:
1. oc new-project my-project
2. Prepare certificate using openssl
   - openssl genrsa -des3 -o CA.key 4096
   - openssl req -new -x509 -nodes -key CA.key -out CA.pem -days 3600
   - openssl x509 -req -in tls.csr -CA CA.pem -CAkey CA.key -CAcreateserial -days 1600 -out tls.crt
3. oc create secret tls hello-app-secret --cert cert/tls.crt --key cert/tls.key
4. oc set volume deploy/hello-app --add --type secret --secret-name hello-app-secret --mount-path /run/secrets/nginx/
5. oc get pods