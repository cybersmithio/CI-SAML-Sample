# Building outside a container

To recompile:
npx webpack --config webpack.server.js --mode=development

npx webpack --config webpack.server.js



# Building the container image


```
docker build -t samltestapp ./ -f Dockerfile
docker run --rm -it --name samltestapp -p 443:443 samltestapp

docker run --rm -it --name samltestapp -p 443:443 --mount type=bind,source=/c/Users/jsmith/VSC/CI-SAML-Sample/.env,target=/usr/src/app/.env samltestapp

docker run --rm -it --name samltestapp -p 443:443 \
    --mount type=bind,source=/c/Users/jsmith/VSC/CI-SAML-Sample/.env,target=/usr/src/app/.env \
    --mount type=bind,source=/c/certs/server.cert,target=/usr/src/app/server.cert \
    --mount type=bind,source=/c/certs/server.key,target=/usr/src/app/server.key \
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
