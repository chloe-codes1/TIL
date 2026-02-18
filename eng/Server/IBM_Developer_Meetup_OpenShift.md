# IBM Developer Meetup - OpenShift World Tour

<br>

<br>

### What is OpenShift?

<br>

- Open Source Application Shift
  - OKD: The Origin Community Distribution of Kubernetes
  - PaaS

<br>

<br>

### OpenShift 4 Platform

- Fully integrated and automated
- Seamless Kubernetes deployment
- Fully automated installation
- 1-click platform updates
- Autoscaling of cloud resources

![image-20200318141512215](../kor/images/image-20200318141512215.png)

<br>

<br>

### Kubernetes vs OpenShift

<br>

> Application Management

| Kubernetes                          | OpenShift                                                    |
| ----------------------------------- | ------------------------------------------------------------ |
| Time needed for cluster setup       | Various Cloud Vendors                                        |
| VM or Baremetal server preparation  | On-Prem and user-configured Servers also via Ansible Playbook |
| Configure Master Node               |                                                              |
| Configure Worker Node               |                                                              |

<br>

> Security

| Kubernetes                                                   | OpenShift                                                |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| Since projects involve people with various permissions        | Provided Out-of-Box                                      |
| RBAC (Roll Based Access Control)                             | Add users to Project and grant permissions               |
| IAM (Integrated Access Management)                           | Restrictions on containers running with root permissions |
| Authentication                                               | Includes security-related elements                       |
| However, various publicly available images can be run immediately | FIPS Compliance                                          |

<br>

> Application Deployment

| Kubernetes                              | OpenShift                                                    |
| --------------------------------------- | ------------------------------------------------------------ |
| Individual application deployment steps | Create App in OpenShift Project                              |
| Write code                              | Create image with Source-to-Image                            |
| Container Image Build                   | Register in Image Stream                                     |
| Registry registration                   | Update App with changed Image                                |
| CI / CD setup                           | Additionally, Jenkins DevOps can be configured through the Dashboard Catalog |
| Application deployment                  |                                                              |

<br>

<br>
