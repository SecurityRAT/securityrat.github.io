---
title: OpenID Connect (OIDC)
#keywords: sample
summary: "Steps for deploying SecurityRAT as an OIDC client."
sidebar: home_sidebar
permalink: int_oidc.html
#simple_map: true
#map_name: usermap
#box_number: 1
folder: product2
---


## OpenID Connect

If you're not familiar with OIDC, please refer to these resources: 

* [Wikipedia Article](https://en.wikipedia.org/wiki/OpenID#OpenID_Connect_(OIDC))
* [project homepage](https://openid.net)


## Integration steps

In order to deploy SecurityRAT as an OIDC client, just open the configuration file at `src/main/resources/config/application.yml` (depending on whether you want to configure the development or production profile) and edit the following lines:

```yaml
application:
  authentication:
    type: OIDC
  oidc:
    issuerUri: http://localhost:8080/realms/example-realm
    clientId: <client-id>
    clientSecret: <client-secret>
    rolesClaimPath: <claim-path> # Inside the openid scope
```

Restart the application and you're done!

The following roles are available: "ROLE_ADMIN", "ROLE_USER" and "ROLE_TRAINER"
Make sure to configure your OIDC proiver to return role claims in the "openid" scope.


{% include links.html %}