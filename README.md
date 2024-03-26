# envoy-http-proxy

### Test calling Service Directly

XSS phase 1
`curl -I 'http://172.19.0.100:9898/anything?arg=<script>alert(0)</script>'`

SQLI phase 2 (reading the body request)
`curl -i -X POST 'http://172.19.0.100:9898/anything' --data "1%27%20ORDER%20BY%203--%2B"`

### Test calling from HAProxy reverse proxy (HAproxy -> Service)

XSS phase 1
`curl -I 'http://172.19.0.4:80/anything?arg=<script>alert(0)</script>'`

SQLI phase 2 (reading the body request)
`curl -i -X POST 'http://172.19.0.4:80/anything' --data "1%27%20ORDER%20BY%203--%2B"`

### Test calling from Envoy with Coraza WAF (Envoy -> HAProxy -> Service)

XSS phase 1
`curl -I 'http://172.19.0.3:80/anything?arg=<script>alert(0)</script>'`

SQLI phase 2 (reading the body request)
`curl -i -X POST 'http://172.19.0.3:80/anything' --data "1%27%20ORDER%20BY%203--%2B"`

### Test calling from Envoy with Coraza WAF (Envoy -> HAProxy -> Service)

XSS phase 1
`curl -I 'http://172.19.0.6:80/anything?arg=<script>alert(0)</script>'`

SQLI phase 2 (reading the body request)
`curl -i -X POST 'http://172.19.0.6:80/anything' --data "1%27%20ORDER%20BY%203--%2B"`
