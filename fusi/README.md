JWT.go:

contains some code doing JWT authentication on HTTP (JSON token according with https://tools.ietf.org/html/rfc7519 )

It runs on localhost:8080 
When you do a post on http://localhost:8080/login , like:

<pre> {"username": "admin",
"password": "mizzega"
}
</pre>
it will return something like:

<pre>
{"token":"averylong.token.here"}
</pre>

From this moment on, putting the token and doing requestes to 

http://localhost:8080/resource

will give you positive answer, like:

<pre>
{"data": "Gained access to protected resource"}
</pre>

else , the URL is forbidden.


Is written in go.

To use it, please Generate RSA signing files via shell (adjust as needed):

- $ openssl genrsa -out app.rsa 1024
- $ openssl rsa -in app.rsa -pubout > app.rsa.pub

and put in the same folder the executable runs.


NEXT STEP: to start it using docker.

