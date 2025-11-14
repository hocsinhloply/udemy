# Table of contents
1. [I. EKS](#eks)
2. [II. Lab](#lab)
3. [III. Basic markdown](#basic-markdown)
4. [IV. CICD](#cicd)

<a name="eks"></a>
# I. EKS

Ref:
- https://docs.aws.amazon.com/eks/latest/userguide/network-reqs.html
- https://github.com/kubernetes-sigs/aws-load-balancer-controller/blob/main/docs/guide/ingress/annotations.md
- https://docs.aws.amazon.com/eks/latest/userguide/sec-group-reqs.html
- https://docs.aws.amazon.com/eks/latest/userguide/sec-group-reqs.html#security-group-restricting-cluster-traffic
- https://docs.aws.amazon.com/eks/latest/userguide/hybrid-nodes-networking.html
- https://docs.aws.amazon.com/eks/latest/best-practices/control-plane.html

Control Plane Components manage the cluster and provide access to its APIs. 
Worker nodes (sometimes just referred to as Nodes) provide the places where the actual workloads are run. 
Node Components consist of services that run on each node to communicate with the control plane and run containers. 
The set of worker nodes for your cluster is referred to as the Data Plane.

Tasks that components of the Kubernetes control plane performs include:

Communicating with cluster components (API server)
Store data about the cluster (etcd key value store)
Schedule Pods to nodes (Scheduler)
Keep components in desired state (Controller Manager)
Manage cloud resources (Cloud Controller Manager)


## Control plane
- The EKS control plane comprises the Kubernetes API server nodes, etcd cluster.
- Kubernetes API server nodes that run components like the API server, scheduler, and kube-controller-manager run in an auto-scaling group.


- Stand for **Elastic Kubernetes Service**
- Way to launch managed Kubernetes clusters on AWS
- Support two launch modes
  - EC2 launch mode (Worker node)
  - Fargate launch mode (serverless container)
- Node Types:
  - Managed Node Groups
  - Self-Managed Nodes
  - AWS Fargate

- Creates an EKS Pod Identity association between **a service account in an Amazon EKS cluster** and **an IAM role with EKS Pod Identity**. Use EKS Pod Identity to give **temporary IAM credentials to Pods** and the credentials are rotated automatically.
- 

<a name="lab"></a>
# II. Lab
1. **Create Cluster IAM role**: Select the Cluster IAM role to allow the Kubernetes control plane to manage AWS resources on your behalf. This cannot be changed after the cluster is created. To create a new custom role, follow the instructions in the Amazon EKS User Guide .
```
AWS Management Console
a. Open the IAM console at https://console.aws.amazon.com/iam/.
b. Choose Roles, then Create role.
c. Under Trusted entity type, select AWS service.
d. From the Use cases for other AWS services dropdown list, choose EKS.
e. Choose EKS - Cluster for your use case, and then choose Next.
f. On the Add permissions tab, choose Next.
g. For Role name, enter a unique name for your role, such as eksClusterRole.
h. For Description, enter descriptive text such as Amazon EKS - Cluster role.
i. Choose Create role.
```
2. **Create VPC, Subnet, SG**
```
Create inbound from bastion for the cluster's SG
```
3. **Create Cluster**
4. **Create Node IAM role**
```
AmazonEC2ContainerRegistryReadOnly
AmazonEKS_CNI_Policy
AmazonEKSWorkerNodePolicy
AmazonSSMManagedInstanceCore
CloudWatchAgentServerPolicy
```
5. **Create Node group**

- Update file config ~/.kube/config. The settings in this file enable the kubectl CLI to communicate with your cluster
```
aws eks update-kubeconfig --region ap-southeast-1 --name {cluster_name}
```
- Confirm that the EKS Pod Identity Agent pods are running on your cluster.
```
kubectl get pods -n kube-system | grep 'eks-pod-identity-agent'
```
- Get cluster info
```
kubectl config get-contexts
kubectl cluster-info
```
- Check IAM Role
```
aws sts get-caller-identity
```
- To verify the user identity
```
aws configure --profile {name_profile}
```
```
kubectl get all -A
```
```
- List ServiceAccount
kubectl get sa 
```
```
kubectl config get-clusters
kubectl config delete-cluster {name}
```


- IAM role, policy attached to Cluster, Nodes, Pods
- Pod Security Policy: Cluster level, manage create, update pod policies
- Role (gán với namespace) vs Cluster Role (Cluster Role cấp quyền cho các đối tượng cấp độ cluster không giới hạn namespace)
- RoleBinding & ClusterRoleBinding gán user với các role tương ứng

- Create cluster (Console and CLI)
1. Create Amazon EKS cluster
   - Create an Amazon VPC, private subnet
   - Create a cluster IAM role. Kubernetes clusters managed by Amazon EKS make **calls to other AWS services** on your behalf to manage the resources that you use with the service.
   - Create cluster in Console ...
2. Configure computer to communicate with your cluster
   - Create a kubeconfig file for your cluster. The settings in this file enable the kubectl CLI to communicate with your cluster.
```
aws eks update-kubeconfig --region region-code --name my-cluster
By default, the config file is created in ~/.kube/config
```
3. Create nodes
   - This procedure configures your cluster to use Managed node groups to create nodes => Create your EC2 Linux managed node group.
   - Create a node IAM role and attach the required Amazon EKS IAM managed policy to it. The Amazon EKS node kubelet daemon makes calls to AWS APIs on your behalf. Nodes receive permissions for these API calls through an IAM instance profile and associated policies.
   - Add Node Group in Compute tab
4. Delete resources
   - Delete any node groups => Delete cluster => Delete VPC AWS CloudFormation => Delete IAM roles


<a name="basic-markdown"></a>
# III. Basic markdown

```
- Anchor point: <a name="my-custom-anchor-point"></a>
- Image: ![Text](link)
- Link: [GitHub Pages](https://pages.github.com/)
- Check list: [ ] \(Optional) Open a followup issue
- Line break: \ or Enter
- Using Emojis: :EMOJICODE:
- Footnotes:
Here is a simple footnote[^1].

A footnote can also have multiple lines[^2].

[^1]: My reference.
[^2]: To add line breaks within a footnote, add 2 spaces to the end of a line.  
This is a second line.

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.
```

<a name="note"></a>
> [!NOTE]
> - Markdown basic: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
> - Application Recovery Controller (ARC)
> - Workloads: Kubernetes defines a Workload as "an application running on Kubernetes." That application can consist of a set of microservices run as Containers in Pods, or could be run as a batch job or other type of applications.
> - ARC option in EKS: https://docs.aws.amazon.com/eks/latest/userguide/zone-shift.html
> - EKS chỉ nhận diện user tạo ra cluster là admin => dù IAM Role có AdministratorAccess cũng không tương tác được với cluster trừ khi phải set up quyền trong cluster
> - role-based access control (RBAC)
> - ServiceAccount là một resource để application bên trong container sử dụng cho việc authenticated tới API server, scope namespace, mỗi namespace có 1 ServiceAccount tên `default`, một ServiceAccount có thể được sử dụng bởi nhiều Pod.
> - ServiceAccount mặc định nếu không bật (RBAC) sẽ có quyền thực hiện mọi hành động lên API => có thẻ list, delete, create Pod => ngăn chặn = cách enable RBAC
> - From version 1.8 default enabled RBAC => can create role and attach for ServiceAccount
> - 

- RBAC action

| Action | Verb     |
|--------|----------|
| HEAD   | get      |
| GET    | get      |
| POST   | create   |
| PUT    | update   |
| PATCH  | patch    |
| DELETE | delete   |

- RBAC resources
  - Roles: định nghĩa verb nào có thể được thực hiện trên namespace
  - ClusterRoles: định nghĩa verb nào có thể được thực hiện trên cluster
  - RoleBindings: gán role tới một SA
  - ClusterRoleBindings: gán ClusterRoles tới SA

```
kubectl get sa // List all service account
kubectl get clusterroles
kubectl get clusterrolebindings
kubectl get clusterrole view -o yaml // List all resources in a namespace
```

# Reference
1. [Kubernetes concepts](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-concepts.html)


<a name="cicd"></a>
# IV. CICD

## 1. CodeBuild
- Một dịch vụ Xây dựng kiểm thử từ AWS
- Chạy kiểm thử và tạo ra các software package
- Mục đích cuối cùng là tạo ra các artifact (Tập hợp các file tĩnh, file jar, file dockerfile)
- Cung cấp file 'buildspec' thông qua một Dockerfile từ source code.
- Bản chất là những EC2 - managed service => Có khả năng mở rộng
- Price: chi phí cho thời gian build

## 2. CodeDeploy
- Dịch vụ triển khai tự động vào các môi trường dịch vụ như: EC2, ECS, Lambda or máy chủ vật lý (cần CodeDeploy agent, thường là dùng Jenkins cho on-premises)
- Triển khai tự động: giảm downtime, tăng tốc độ triển khai
- Triển khai môi trường phức tạp
- Khả năng tích hợp
- Quản lý chi phí
- Cập nhật liên tục

## 3. CodePipeline
- Dịch vụ giúp tự động hóa các bước trong quá trình phát triển phần mềm.
- Xác định một chuỗi các bước "pipeline" mỗi bước được thực hiện khi code thay đổi
- VD: thay đổi code trong kho lưu trữ (Git, Github, ...)

## 4. Github Action

Workflow triggers are events that cause a workflow to run. These events can be:
- Events that occur in your workflow's repository
- Events that occur outside of GitHub and trigger a repository_dispatch event on GitHub
- Scheduled times
- Manual

Example:
```
- Trigger when have a pull_request event
on:
  pull_request:
    # Sequence of patterns matched against refs/heads
    branches:
      - main

- Trigger when have a push event
on:
  push:
    branches:
      - main
      - 'releases/**'




```


















