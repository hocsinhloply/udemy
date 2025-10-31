# Table of contents
1. [I. EKS](#eks)
2. [II. Lab](#lab)
3. [III. Basic markdown](#basic-markdown)

<a name="eks"></a>
# I. EKS

<a name="lab"></a>
# II. Lab
- Create Cluster IAM role: Select the Cluster IAM role to allow the Kubernetes control plane to manage AWS resources on your behalf. This cannot be changed after the cluster is created. To create a new custom role, follow the instructions in the Amazon EKS User Guide .
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
> - Workloads: applications
> - ARC option in EKS: https://docs.aws.amazon.com/eks/latest/userguide/zone-shift.html
