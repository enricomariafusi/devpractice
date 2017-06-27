JWT.go:

contains some code doing JWT authentication on HTTP (JSON token according with https://tools.ietf.org/html/rfc7519 )

It runs on port 8080, you can check on localhost when you don't use docker. 
When you do a post on http://localhost:8080/login , like:

<pre> {"username": "admin",
"password": "mizzega"
}
</pre>
it will return something like:

<pre>
{"token":"averylong.token.here"}
</pre>

From this moment on, if you do a request here, with an extraheader like:

<pre>
Authorization: Bearer averylong.token.here
</pre>

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


NEXT STEP: to start it using docker using the "generic" driver.

Install docker in your computer. I assume the docker main service is up and running.

Create a folder like "myimage" into the folder you keep your images.

cd ~/somewhere/myimage

touch Dockerfile

copy the executable you created from the source, like: cp mizzega-jwt ~/somewhere/myimage

edit dockerfile:

<pre>
FROM boot2docker
MAINTAINER your@email
RUN mkdir -p /opt/bin
ADD . /opt/bin/
CMD ["/opt/bin/mizzega-jwt"]
EXPOSE 8080
</pre>

write:

<pre>
docker build --tag=mizzega-jwt .
</pre>

Now you created the image yu can list it

<pre>
docker images
</pre>

And you can run it

<pre>
docker run -p portIlike:8080 mizzega-jwt
</pre>

