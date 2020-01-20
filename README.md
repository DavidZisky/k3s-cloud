# k3s-cloud

[k3s](https://k3s.io/) allows you to spin up Kubernetes cluster in seconds. Unfortunately it does not come with cloud providers support so you can't use cloud LB/DNS/storage. This repo shows (and provides ready to use solutions too) how to integrate [CCM](https://kubernetes.io/docs/tasks/administer-cluster/running-cloud-controller/) with k3s.


# What does it mean

It means that your k3s cluster can behave like managed Kubernetes so for example whenever you deploy service type LoadBalancer, the real LoadBalancer will be created and configured

# Solution

Please follow instructions below depending on the cloud provider you want to use. For now only DigitalOcean support. The rest coming soon.

## DigitalOcean
### Prerequisites

For DigitalOcean the only thing you need is token ([How to get token](https://www.digitalocean.com/docs/api/create-personal-access-token/)) and ssh key fingerprints. DO cli is not required.

REQUIREMENTS:

1. Make sure you have [jq](https://stedolan.github.io/jq/) installed
2. Add your DigitalOcean API Token and SSH Key fingerprint in .env file


USAGE:

1. Make sure You fill requirements above
2. Simply execute ./k3s_deployer_cloudmanag.sh
3. After ~3-5 minutes your cluster is ready and kubectl config is loaded into your system - you can start using it :)

Since k3s uses Traefik, while deploying k3s the DigitalOcean Load Balancer will be created anbd configured to point to Traefik. If you now deploy any deployment with Service and Ingress - traffic will be sent via DO LB to your k3s cluster. See example_deployment for reference.
