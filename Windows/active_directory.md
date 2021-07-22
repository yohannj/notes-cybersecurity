# Overview
Active Directory is a collection of machines and servers connected inside of domains, that are a collective part of a bigger forest of domains, that make up the Active Directory network.

This collection include, but is not limited to:
* Domain Controllers
* Forests, Trees, Domains
* Users + Groups 
* Trusts
* Policies 
* Domain Services

# Services
## Domain Controllers
A domain controller is a Windows server that has Active Directory Domain Services (AD DS) installed and has been promoted to a domain controller in the forest. Domain controllers are the center of Active Directory -- they control the rest of the domain.

It:
* holds the AD DS data store 
* handles authentication and authorization services 
* replicate updates from other domain controllers in the forest
* Allows admin access to manage domain resources

### AD DS Data Store
The Active Directory Data Store holds the databases and processes needed to store and manage directory information such as users, groups, and services. Below is an outline of some of the contents and characteristics of the AD DS Data Store:
* Contains the NTDS.dit - a database that contains all of the information of an Active Directory domain controller as well as password hashes for domain users
* Stored by default in %SystemRoot%\NTDS
* accessible only by the domain controller

## Forest
Group of domain trees inside an AD network. It contains:
| Domain tree type           | Description                                                     |
| -------------------------- | --------------------------------------------------------------- |
| Trees                      | A hierarchy of domains in Active Directory Domain Services      |
| Domains                    | Used to group and manage objects                                |
| Organizational Units (OUs) | Containers for groups, computers, users, printers and other OUs |
| Trusts                     | Allows users to access resources in other domains               |
| Objects                    | users, groups, printers, computers, shares                      |
| Domain Services            | DNS Server, LLMNR, IPv6                                         |
| Domain Schema              | Rules for object creation                                       |

### Users
4 main types of users:
* Domain Admins
* Service Accounts (used only in rare cases)
* Local Administrators --> No access to Domain Controller
* Domain Users

### Groups
2 types of groups:
* Security Groups --> Used to specify permissions for a large number of users
* Distribution Groups --> Used for email distribution lists

#### Default security groups
| Security group name                     | Description                                                                                                      |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Domain Controllers                      | All domain controllers in the domain                                                                             |
| Domain Guests                           | All domain guests                                                                                                |
| Domain Users                            | All domain users                                                                                                 |
| Domain Computers                        | All workstations and servers joined to the domain                                                                |
| Domain Admins                           | Designated administrators of the domain                                                                          |
| Enterprise Admins                       | Designated administrators of the enterprise                                                                      |
| Schema Admins                           | Designated administrators of the schema                                                                          |
| DNS Admins                              | DNS Administrators Group                                                                                         |
| DNS Update Proxy                        | DNS clients who are permitted to perform dynamic updates on behalf of some other clients (such as DHCP servers). |
| Allowed RODC Password Replication Group | Members in this group can have their passwords replicated to all read-only domain controllers in the domain      |
| Group Policy Creator Owners             | Members in this group can modify group policy for the domain                                                     |
| Denied RODC Password Replication Group  | Members in this group cannot have their passwords replicated to any read-only domain controllers in the domain   |
| Protected Users                         | Members of this group are afforded additional protections against authentication security threats.               |
| Cert Publishers                         | Members of this group are permitted to publish certificates to the directory                                     |
| Read-Only Domain Controllers            | Members of this group are Read-Only Domain Controllers in the domain                                             |
| Enterprise Read-Only Domain Controllers | Members of this group are Read-Only Domain Controllers in the enterprise                                         |
| Key Admins                              | Members of this group can perform administrative actions on key objects within the domain.                       |
| Enterprise Key Admins                   | Members of this group can perform administrative actions on key objects within the forest.                       |
| Cloneable Domain Controllers            | Members of this group that are domain controllers may be cloned.                                                 |
| RAS and IAS Servers                     | Servers in this group can access remote access properties of users                                               |
