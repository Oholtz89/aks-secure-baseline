# Prep for Azure Active Directory Integration

In the prior step, you [generated the user-facing TLS certificate](./02-ca-certificates.md); now we'll prepare Azure AD for Kubernetes role-based access control (RBAC). This will ensure you have an Azure AD security group(s) and user(s) assigned for group-based Kubernetes control plane access.

## Expected results

Following the steps below you will result in an Azure AD configuration that will be used for Kubernetes control plane (Cluster API) authorization.

| Object                         | Purpose                                                 |
|--------------------------------|---------------------------------------------------------|
| A Cluster Admin Security Group | Will be mapped to `cluster-admin` Kubernetes role.      |
| A Cluster Admin User           | Represents at least one break-glass cluster admin user. |
| Cluster Admin Group Membership | Association between the Cluster Admin User(s) and the Cluster Admin Security Group. |
| _Additional Security Groups_   | _Optional._ A security group (and its memberships) for the other built-in and custom Kubernetes roles you plan on using. |

## Steps

> :book: The Contoso Bicycle Azure AD team requires all admin access to AKS clusters be security-group based. This applies to the new Secure AKS cluster that is being built for Application ID a0008 under the BU001 business unit. Kubernetes RBAC will be AAD-backed and access granted based on a user's AAD group membership.

1. Query and save your Azure subscription's tenant id.

   ```bash
   TENANTID_AZURERBAC=$(az account show --query tenantId -o tsv)
   ```


1. Your team has created Azure AD security group that is going to map to the [Kubernetes Cluster Admin](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#user-facing-roles) role `cluster-admin`. Please assigned the following variables with the information for your organization:

   ```bash
   AADOBJECTNAME_GROUP_CLUSTERADMIN=
   AADOBJECTID_GROUP_CLUSTERADMIN=
   TENANTDOMAIN_K8SRBAC=
   TENANTID_K8SRBAC=
   AADOBJECTNAME_USER_CLUSTERADMIN=
   AADOBJECTID_USER_CLUSTERADMIN=
  
   ```

   The AADOBJECTID_GROUP_CLUSTERADMIN object ID will be used later while creating the cluster. This way, once the cluster gets deployed the new group will get the proper Cluster Role bindings in Kubernetes.

### Next step

:arrow_forward: [Deploy the hub-spoke network topology](./04-networking.md)
