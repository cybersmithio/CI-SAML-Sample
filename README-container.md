# Building outside a container

To recompile:
npx webpack --config webpack.server.js --mode=development

npx webpack --config webpack.server.js

npm start

# Building the container image


```
docker build -t samltestapp ./ -f Dockerfile
```

# Running the container image

Create a .env file on the host system.  It will hold the initial configuration for the container:
```
SASS_PATH="node_modules"
SKIP_PREFLIGHT_CHECK=true
REACT_APP_HOSTNAME=https://hostname.domain.tld
REACT_APP_ENTITYID=sample-saml-app
REACT_APP_SHOWSETUP=true
REACT_APP_HTTPS=true
PORT=443
```

To run on port 443 and with the above configuration.  (The path will vary based on your system.)
```
docker run --rm -it --name samltestapp -p 443:443 --mount type=bind,source=/data/.env,target=/usr/src/app/.env samltestapp
```

If the federation configuration is already known, you can also create a properties.json file on the host such as this:
```
{
  "loginurl": "https://idp.domain.tld/isam/sps/sample-saml-app/saml20/login",
  "logouturl": "https://idp.domain.tld/pkmslogout",
  "certificate": "-----BEGIN CERTIFICATE-----\n*************==\n-----END CERTIFICATE-----\n"
}
```

And then mount the properties file into the system as well:
```
docker run --rm -it --name samltestapp -p 443:443 --mount type=bind,source=/data/.env,target=/usr/src/app/.env --mount type=bind,source=/data/properties.json,target=/usr/src/app/properties.json samltestapp
```

If the application needs a signed certificate and private key, these can be mounted into the container in the /usr/src/app/ directory.  The server.cert and server.key files are neede:

```
docker run --rm -it --name samltestapp -p 443:443 \
    --mount type=bind,source=/data/.env,target=/usr/src/app/.env \
    --mount type=bind,source=/data/certs/server.cert,target=/usr/src/app/server.cert \
    --mount type=bind,source=/data/certs/server.key,target=/usr/src/app/server.key \
    samltestapp
```

Go to https://localhost/.  You must use HTTPS or the cookies will not set properly for this to work.



# Examine a new container
docker run --rm -it --name samltestapp -p 443:443 samltestapp sh

# Examine a running container
docker exec -it samltestapp sh

# Export and import
docker image save samltestapp -o samltestapp.tar
docker image load -i samltestapp.tar
