# Set up Jenkins, configure Docker as a build agent, implement a CI/CD pipeline, and deploy applications to Kubernetes using Argo CD following a GitOps approach.

<img width="1982" height="989" alt="image" src="https://github.com/user-attachments/assets/48618647-5352-4ca4-91d6-fec40127e874" />

# Pre-requisite:
An EC2 instance 

# Tools for installation:
- Java 21
- maven
- docker
- Jenkins
- SonarQube
- Argo CD
- Minikube
- kubectl

The application that we are going to deploy as part of this project

<img width="2400" height="1260" alt="image" src="https://github.com/user-attachments/assets/db7c676f-82f3-4a9c-8c0c-d50d909c0bca" />


# The CI Part: [Jenkins]

( Install the necessary plugins such as docker pipeline plugin, github plugin and add the credentials for SQB, Docker and GitHub)

<img width="2400" height="783" alt="image" src="https://github.com/user-attachments/assets/1f351632-8149-466c-8fe2-d55a7f9df49a" />

- Developer commits to git repo
- Webhooks configured triggers the jenkins pipeline
- Jenkins pipeline : Build the code using Maven, Code quality analysis using SQB, Run the tests (send notifications upon failure)

<img width="2400" height="1260" alt="image" src="https://github.com/user-attachments/assets/bb476c29-75ec-4817-a60a-a0d6fe8ce240" />
<img width="2400" height="1260" alt="image" src="https://github.com/user-attachments/assets/ef927e05-0153-464d-9468-5c234826232d" />


# The CD Part: [Argo CD]

Create a namespace argocd

Install Argo CD and create controllers

<img width="2391" height="672" alt="image" src="https://github.com/user-attachments/assets/b1f42b47-b400-4fde-b2c8-e545c8c9b5c6" />

To access the UI of Argo CD, change the service type of argocd-server from ClusterIP to NodePort

<img width="1925" height="1019" alt="image" src="https://github.com/user-attachments/assets/ec01b167-0fda-4c56-b4bc-334f32e7b5ab" />


- image of our application is pushed to DockerHub by the pipeline
<img width="1608" height="167" alt="image" src="https://github.com/user-attachments/assets/532daabf-70c6-47d5-ab49-77236a21dd4c" />
<img width="2400" height="1170" alt="image" src="https://github.com/user-attachments/assets/2b949518-1ad0-4e1e-8282-1c3edf15412f" />

- Shell script picks it up and updates with the new image in manifest repo (deployment file)

  
before updation

<img width="2025" height="1193" alt="image" src="https://github.com/user-attachments/assets/956a1296-95d7-4cd2-bd66-c425167f5a64" />


after updation

<img width="2025" height="1233" alt="image" src="https://github.com/user-attachments/assets/b4fd4592-b8eb-4f05-8574-c2bb232d9b02" />

- Argo CD (a GitOps tool) detects the change and deploys it to the K8S cluster

<img width="1364" height="737" alt="image" src="https://github.com/user-attachments/assets/82cc3357-0608-4044-9493-f8466359727e" />
<img width="2400" height="1260" alt="image" src="https://github.com/user-attachments/assets/10182349-bc13-4fd7-a072-ded44281fb9e" />
<img width="2400" height="1260" alt="image" src="https://github.com/user-attachments/assets/a35dcf1d-f2ac-4d95-af21-1794e2a03f7c" />

