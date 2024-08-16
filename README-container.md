# Building outside a container

To recompile:
npx webpack --config webpack.server.js --mode=development

npx webpack --config webpack.server.js



# Building the container image


```
docker build -t samltestapp ./ -f Dockerfile
docker run --rm -it --name samltestapp -p 3006:3006 samltestapp
```

Go to https://localhost:3006/.  You must use HTTPS or the cookies will not set properly for this to work.



# Examine a new container
docker run --rm -it --name samltestapp -p 3006:3006 samltestapp sh

# Examine a running container
docker exec -it samltestapp sh

# Export and import
docker image save samltestapp -o samltestapp.tar
docker image load -i samltestapp.tar
