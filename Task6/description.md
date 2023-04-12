## Task 6: Creating a Pass through route
- Create a pass through route to the hello-app service, which points to hello-app-my-project.apps-crc.testing
- Use curl --insecure https://hello-app-my-project.apps-crc.testing to verify that the route responds to external requests

### Solution:
1. oc create route passthrough hello-app --hostname=hello-app-my-project.apps-crc.testing --service=hello-app