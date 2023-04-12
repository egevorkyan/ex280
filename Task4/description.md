## Task 4: Creating a Project
- As the user developer, create a project with the name local-project. Ensure that
  this project inherits settings from the new project template created in Task 3.

### Solution:
1. oc login -u developer -p <PASSWORD>
2. oc new-project local-project
3. oc describe project local-project
4. oc get networkpolicy
5. output.txt shows output from command 3 and 4, take a look on quota, limit range sections. Also network policies inherited.