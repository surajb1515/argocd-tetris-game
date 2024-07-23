# Tetris Game on Kubernetes using ArgoCD

Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular service providers as well as custom in-house solutions.

The key features of Terraform are:

- **Infrastructure as Code**: Infrastructure is described using a high-level configuration syntax. This allows a blueprint of your datacenter to be versioned and treated as you would any other code. Additionally, infrastructure can be shared and re-used.
- **Execution Plans**: Terraform has a "planning" step where it generates an execution plan. The execution plan shows what Terraform will do when you call apply. This lets you avoid any surprises when Terraform manipulates infrastructure.
- **Change Automation**: Complex changesets can be applied to your infrastructure with minimal human interaction. With the previously mentioned execution plan and resource graph, you know exactly what Terraform will change and in what order, avoiding many possible human errors.

## What is GitOps?

Modern and cloud-native applications are developed with speed and scale in mind. Organizations with a mature DevOps culture can deploy code to production hundreds of times per day. DevOps teams can accomplish this through development best practices such as version control, code review, and CI/CD pipelines that automate testing and deployments.

- **IaaC**: Automating infrastructure provisioning through GitOps involves storing configuration files as code, similar to how application source code is utilized.
- **CI/CD**: GitOps automates infrastructure updates with Git workflows, including CI/CD. Changes are applied automatically, and GitOps overwrites any drift. GitLab uses CI/CD for automation, but other types, like definition operators, can be used too.
- **Single source of truth**: GitOps uses Git as the single source of truth to define a cloud-native system. GitOps agent (Flux) applies to code, configuration, and policies across all environments.

## Prerequisites

1. [AWS Account](https://aws.amazon.com/account/)
2. [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
3. [Install Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
4. [Configure AWS credentials](https://docs.aws.amazon.com/cli/v1/userguide/cli-chap-configure.html)
5. [GitLab Account](https://gitlab.com)

## Terraform Commands

```bash
terraform init
terraform validate
terraform plan
terraform apply --auto-approve
terraform destroy --auto-approve
```

![Untitled](/Images/terraform-apply.png)

## Achitecture of AWS EKS Cluster and ArgoCD

![Untitled](/Images/eks.png)
![Untitled](/Images/argocd-arch.png)

## To setup ArgoCD on Kubernetes

```bash
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

To expose ArgoCD UI

```bash
kubectl port-forward -n argocd svc/argocd-server 8080:443


# username is admin
# and for password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

```

![suraj](/Images/argocd-ui.png)

Now Create new application in argocd using github repo link

![suraj](/Images/argocd-2.png)
![suraj](/Images/argocd-3.png)
![suraj](/Images/terminal-1.png)

### Finally the tetris is deployed on the public AWS LoadBalancer

![suraj](/Images/game-2.png)
