# EC2 Traefik Demo

This is a demo project to show how to deploy a working traefik instance on Amazon EC2

## Using this repository as an example

This repository includes a devcontainer configuration which includes all required tools to deploy the traefik instance.

Clone / fork or copy this repository. After setting up your EC2 instance with SSH access follow these steps:

1. Update `ansible_host` and the hostname `demo_ec2_server` in `ansible/host.yml`.
1. Set a traefik dashboard password using a secret manager (like ansible-vault) in `ansible/host_vars/<hostname>/vars.yml` or remove all dashboard configurations.
1. Set the Email address in `ansible/docker-project-deployment/files/traefik.yml` for the `httpresolver`.
1. Run the playbook from the `ansible` directory.

It will:
- Install `docker` and enable the system service
- Add a new user named `docker-user`
- Add both the ec2-user (or other configured `ansible_user`) and the created `docker-user` to the `docker` group.
- Install the docker-compose cli-plugin
- Deploy traefik and a docker socket proxy to `/opt/project_deployment_projects/traefik` using the `docker-user`.
