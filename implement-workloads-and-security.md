# Implement workloads and security (20-25%)

## Migrate servers to Azure

## Configure serverless computing

## Implement application load balancing

## Integrate on-premises network with Azure virtual network

## Implement Multi-Factor Authentication (MFA)

## Manage role-based access control (RBAC)

### Goal

* Create a custom role
* Configure access to azure resources by assigning roles
* Configure management access to Azure
* Troubleshoot RBAC
* Implement Azure policies
* Assign RBAC roles

### RBAC

#### Security Principal

* An Object that represents an individual, collection of individuals, an application or service that requires access to an azure resource.
* Individuals are represented as Azure AD Users and Users in other tenancies.
* Collections of Individuals are represented by Azure AD Groups.
* Applications and services are represented by service principals.

#### Role Definition

* A collection of permissions
* A Role definition is expressed as a set of operations that can be performed
* Examples: Read, Write, Delete

##### Scope

* Role definition is the boundary that access applies to.
* Can be assigned at the following levels:
  * Management group
  * Subscription
  * Resource group
  * Resource
* Structured in a parent-child relationship
  * Access at parent scope is inherited at child scope

##### Role Assignment

Is the process of chosing a Security Principal (Identity), Role Definitions (Collection of permissions), and Scope (where the access applies).

#### Why RBAC

* Ensure that the principle of least privilger is used
  * Only required access is granted
  * Minimize damage during account compromise
* Reduce chance of unauthorized actions being permormed
* Reduce chance of accidental actions being performed

#### How RBAC Determines Access

1. Security Pricipal acquire token for ARM
2. REST API call made to ARM with token attached
3. ARM retrieves all role assignments and denies assignments that apply to resources against which action is occuring
4. ARM determines role assignments that apply to security principal for this resource
5. ARM determines if the action in the API call is included in the roles the security principal has for resource
6. If the security principal doesn't have a role with that action in the requested scope, access not granted
7. If deny assignment applies, access is blocked

#### RBAC Drawbacks

* Increases in security impose necessary limitations
* Selecting roles for users requires a good understanding of the specific tasks that individuals need to be able to perform
  * Only provision previleged users with specific tools rather than entire toolbox
  * May mean that extra time is required when nature and scope of the task to be carried out is misjudged

##### Azure AD Admin roles are different from Azure RBAC roles

* Use Azure RBAC roles to manage permissions to Azure resources
* Use Azure AD administrator roles to manage permissions to Azure AD resources

### Azure RBAC Roles

A Role Definition is

* A collection of permissions
* Lists the operations that can be permormed

#### Deny assignments

* Initial version of RBAC was **allow-only** with no **Deny**
* Deny assignment binds a set of deny actions to user/group/service principal at a particular scope for the purpose of denying access
* Can also exclude principals and prevent inheritance to child scopes
* Deny assignments are read-only
* Can apply to the Everone principal
  * Everone principal represents all principals in an azure AD Directory
  * Everone principal uses the Zero GUID

##### Management and Data Operations

Management Operations | Data Operations
----------------------|-----------------
Specified ub the **Actions** and **NotActions** properties if a role definition | Specified in the **DataActions** and **NotDataActions** properties of a role definition
Examples <br>Manage access to storage account<br>Create, update, or delete blob container<br>Delete a resource group and iuts contents |Examples <br>Read a list of blobs in a container<br>Write to a storage blob in a container<br>Delete a message in a queue

