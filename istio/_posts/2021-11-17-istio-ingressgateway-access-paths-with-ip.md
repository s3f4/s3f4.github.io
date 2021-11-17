---
layout: post
title:  "Istio Ingress Gateway Access Paths With IP Address"
date:   2021-11-17 14:43:07 +0300
categories: istio
---
In order to deny accessing to a path from other ip address, istio allows creating role based accesss with ip address. This policy does deny all get requests except specified ip address.

```yaml
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: panel-policy
  namespace: istio-system
spec:
  selector:
    matchLabels:
      app: istio-ingressgateway
  action: DENY
  rules:
    - from:
        - source:
            notRemoteIpBlocks: ["ip address"]
      to:
        - operation:
            paths:
              - "/your-path/*"
            methods: ["GET"]
```


