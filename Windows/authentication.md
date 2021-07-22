# Local authentication
﻿Local authentication is done using the Local Security Authority (LSA). LSA is a protected subsystem that keeps track of the security policies and the accounts that are on a computer system. It also maintains information about all aspects of local security on a computer.

# Active Directory
## On-Premise Active Directory (AD)
Records all authentications + validate authorization.
It uses one of the following protocol:
- NTML
- LDAP / LDAPS
- Kerberos

### NTLM
Kind of a handshake way.
On first call, server returns a challenge that caller needs to solve.

### LDAP / LDAPS
Send creds to Active Directory through LDAP API.

### Kerberos
Kind of a complex handshake way using a third party.
The whole purpose is to get a session key from the Active Directory before contacting a server.

#### Lexical
KDC: Key Distribution Center
SPN: Service Principal Name
TGS: Ticket Granting Service
TGT: Authentication Ticket

#### Accessing a service
Client call KDC to ask a TGT.
KDC verifies creds and then send encrypted TGT (encrypted with TGS secret key) + session key.
Client store TGT until expiration (will then ask a new one)

To connect to a service, Client send TGT to TGS, specifying the SPN he wants to access.
TGS sends back a session key to access the service.

## Azure Active Directory ﻿(AAD)
Contains users and groups. The former connects with a username and a password to access numerous services.

It uses one of the following methods:
- SAML (Security Assertion Markup Language)
- OAuth 2.0
- OpenID Connect

### SAML
It is a Single Sign-On (SSO) authentication.
Identity Providers authenticates a user that will then get access to different Service Providers.

### OAuth 2.0
Authentication is done with an authorization server that returns an access token.
This token can then be used against a resource server (an application) that will validate the token and perform the wanted action.

### OpenID Connect (OIDC)
On top of OAuth 2.0 with an additional ID token.
