# Building the container image



```
docker build -t samltestapp ./ -f Dockerfile
docker run --rm -it --name samltestapp -p 3000:3000 samltestapp
```




# Debugging
docker run --rm -it --name samltestapp -p 3000:3000 samltestapp /bin/sh

# Export and import
docker image save samltestapp -o samltestapp.tar
docker image load -i samltestapp.tar
