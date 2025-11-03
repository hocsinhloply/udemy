# Table of contents
1. [I. EKS](#eks)
2. [II. Lab](#lab)
3. [III. Basic markdown](#basic-markdown)

<a name="eks"></a>
# I. EKS

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

# Reference
1. [Kubernetes concepts](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-concepts.html)
