# mediawiki_helm_repo
This is helm repository to setup mediawiki on Azure Kubernetes Service.

![image](https://github.com/inaushad/mediawiki_helm_repository/assets/47270866/85b36fd3-038c-413e-a284-4a7066dfec21)


Steps to install.

Prerequisites:
1. Setup an AKS Cluster
2. Setup VM to act as a bastion host and connect to AKS Cluster.
3. Install kubectl, helm, docker and git on the VM.

Step 1: Clone the repository from main branch.
Step 2: Build the docker image using ./Dockerfiles/Dockerfile using an appropriate image tag with the container registry name.
Step 3: Push the docker image to container registry by manually loging in using "docker login <registry_url>" or by creating a docker config file.
        Follow: https://docs.docker.com/reference/cli/docker/config/
Step 4: Create a namespace in K8s using "kubectl create namespace <namespace_name>".
Step 5: Create a secret in the K8s namespace for container registry.
        kubectl create secret docker-registry <secret_name> \
                --docker-server=<registry_url> \
                --docker-username=<username> \
                --docker-password=<password> \
                --docker-email=<email_id> \
                --namespace <k8s_namespace>
Step 6: Open values.yml and fill in the details for image(with tag), MySQL and container registry secret.
Step 7: Once all configuration is done, run "helm install <release_name> <chart_folder_name>" (i.e. mediawiki_helm_repository)
Step 8:  This will create pods, services, volumes, deployments for mediawiki webapp and mysql. Use webapp loadbalancer ip/host to access the MediaWiki.





