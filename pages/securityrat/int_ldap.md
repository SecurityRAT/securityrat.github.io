---
title: Lightweight Directory Access Protocol (LDAP)
#keywords: sample
summary: "Steps for deploying SecurityRAT as an LDAP client."
sidebar: home_sidebar
permalink: int_ldap.html
#simple_map: true
#map_name: usermap
#box_number: 1
folder: product2
---


## Lightweight Directory Access Protocol

If you're not familiar with LDAP, please refer to these resources: 

* [Wikipedia Article](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol)
* [project homepage](https://ldap.com/)


## Integration steps

In order to deploy SecurityRAT as a LDAP client, just open the configuration file at `src/main/resources/config/application.yml` (depending on whether you want to configure the development or production profile) and edit the following lines:

```yaml
authentication:
  type: LDAP # possible values are CAS, FORM, LDAP or AZURE
  registration: true # restrict the registration only to the administrators by setting the value to 'false'
ldap:
  url: ldap://ldaptest.example.com:389
  managerDN: cn=technicaluser,ou=users,dc=example,dc=com # Principal or technical user that is used to connect to the LDAP
  managerPassword: neverSaveAPasswordInAConfigFile
  userBaseDN: ou=users,dc=example,dc=com
  userSearchFilter: (&(uid={0})(objectClass=organizationalPerson))
  groupBaseDN: ou=access groups,dc=example,dc=com
  groupSearchFilter: member={0}
  #groupRoleAttribute: # Attribute that contains the role name of an LDAP group. Default: cn
  # Grants the corresponding roles if the user is member of a group with the mentioned groupRoleAttribute
  # If no group is assigned, the corresponding role is automatically given to every authenticated user
  groupOfAdmins: admin-group
  groupOfTrainers: trainer-group
  #groupOfUsers:
```

Restart the application and you're done!


{% include links.html %}