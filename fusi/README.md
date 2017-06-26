JWT.go:

contains some code doing JWT authentication on HTTP (JSON token according with https://tools.ietf.org/html/rfc7519 )

written in go.

First: Generate RSA signing files via shell (adjust as needed):

- $ openssl genrsa -out app.rsa 1024
- $ openssl rsa -in app.rsa -pubout > app.rsa.pub


NEXT STEP: to start it using docker.

