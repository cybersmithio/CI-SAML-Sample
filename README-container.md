# Building the container image



```
docker build -t samltestapp ./ -f Dockerfile
docker run --rm -it --name samltestapp -p 3006:3006 samltestapp
```




# Debugging
docker run --rm -it --name samltestapp -p 3006:3006 samltestapp sh
docker exec -it samltestapp sh

# Export and import
docker image save samltestapp -o samltestapp.tar
docker image load -i samltestapp.tar
