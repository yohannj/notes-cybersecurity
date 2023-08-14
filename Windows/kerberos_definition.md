# Glossary
## TGT - Ticket Granting Ticket
Authentication ticket used to request service tickets from the TGS for specific resources from the domain.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
| Abbr           | Full name                       | Comment                                                                                                                                                                    |
|----------------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AS             | Authentication Service          | Issues TGTs to be used by the TGS in the domain to request access to other machines and service tickets.                                                                   |
| Client LT Key  | Client Long Term Secret Key     | Used to check the encrypted timestamp and encrypt the session key.                                                                                                         |
| KDC            | Key Distribution Center         | Service for issuing TGTs and service tickets that consist of the Authentication Service and the Ticket Granting Service.                                                   |
| KDC LT Key     | KDC Long Term Secret Key        | Used to encrypt the TGT and sign the PAC.                                                                                                                                  |
| PAC            | Privilege Attribute Certificate | Holds all of the user's relevant information, it is sent along with the TGT to the KDC to be signed by the Target LT Key and the KDC LT Key in order to validate the user. |
| Service LT Key | Service Long Term Secret Key    | Used to encrypt the service portion of the service ticket and sign the PAC.                                                                                                |
| Session Key    | Session Key                     | The user will provide the session key to the KDC along with the TGT when requesting a service ticket.                                                                      |
| SPN            | Service Principal Name          | ID given to a service instance to associate it with a domain service account. (Required by Windows)                                                                        |
| TGS            | Ticket Granting Service         | Takes the TGT and returns a ticket to a machine on the domain.                                                                                                             |
| TGT            | Ticket Granting Ticket          | Authentication ticket used to request service tickets from the TGS for specific resources from the domain.                                                                 |
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

![](kerberos_in_a_nutshell.png)