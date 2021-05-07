# Challenge 1

    Goal:  Create 3 tier env and all its resources on Kubernetes in a reproducable and configurable manner
        1. webapp (presentation layer)
        2. python app (business logic layer)
        3. mysql db (data layer)

    This is just a simple example of a solution for creating resources - deployments/pods, services, secrets, configmaps on Kubernetes, executed via ansible-playbook.
    However the deployment itself does not have any meaningful functionality (webapp and python app are bare bone nginx and python images).
    Obviously, actual deployment would require custom built images for presentation and business logic layer.

    Prereq:
        - Docker Desktop is installed with Kubernetes enabled
        - Ansible Engine is installed

    Example execution:

        1. Deployment (create all resources):
            ansible-playbook -i inventory/docker-desktop.yml -v deploy.yml --vault-password-file .ansible_vault
        2. Destroy (delete all resources):
            ansible-playbook -i inventory/docker-desktop.yml -v destroy.yml --vault-password-file .ansible_vault

    This can be further automated by using Jenkins but it would require additional setup/work.
    However, you can find draft Jenkinfile in the repo as well.
