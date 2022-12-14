# Pachchek Sinthuja

# Computational Research Workflows Homework
## Doctoral Programme in Science and Engineering (DSSE)

## Practicalities


## Setting up a git version control repository
```
git init
git add --all
git commit -m "Pushing all files to git";
git branch -M main
git remote add origin https://github.com/pachchek/jhale-computational-workflows-homework.git
git push -u origin main
```
## Dockerfile

1. Create a file `Dockerfile` in the repository containing the following text.

```
FROM ubuntu

RUN sudo apt update && \
    apt-get -y update && \
    apt-get install -y python3-minimal python3-ipython python3-pytest python3-numpy && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
```

2. `git add` and `git push` the file `Dockerfile` to the repository.

```
touch Dockerfile
git add --all
git commit -m "Pushing all files to git"
git branch -M main
git push -u origin main

```

## Build and push Docker image

1. `docker build`, `docker login` and `docker push` the image described by the
   `Dockerfile` to the Dockerhub. Tag your Docker image
   `<yourdockerhubusername>/computational-workflows`.

```
docker build .
docker images
docker tag a524d699d2e6 pachchek/computational-workflows
git add --all
git commit -m "Pushing all files to git"
git push -u origin main

```

## Run a container, and share in files from the host.

1. `docker run` the image. Use the `-v` flag to share the root of the git
   repository to `/root/shared` inside the container. Use the `-ti` flag to get
   an interactive prompt inside the running container.

```
docker run -ti -v $(pwd):/root/shared pachchek/computational-workflows bash

```

## Setup a simple Python test suite

1. In a terminal running on the host (outside the container), copy across the
   files ``wallet.py`` and
   ``test_wallet.py`` to the root of your homework
   repository.  ``git add``, ``git commit`` and ``git push`` them.

```
cp ../computational-workflows-homework-master/wallet.py .
cp ../computational-workflows-homework-master/test_wallet.py .
git add --all
git commit -m "Pushing all files to git"
git push -u origin main

```

2. Start a Docker container using your image and share your repository into a
   directory `/root/shared` into the container.

```
docker run -ti -v $(pwd):/root/shared pachchek/computational-workflows bash
cd /root/shared
```

3. Run the tests inside the container by going to `/root/shared` and running the
   command `py.test-3`. The tests should fail.

3. In a terminal on the host modify ``wallet.py`` until the tests in
   ``test_wallet.py`` all pass.

4. ``git add``, ``git commit`` and ``git push`` the working ``wallet.py`` file.

## GitHub Actions for Continuous Integration

1. Using the example in the class notes make a `.github/workflows/test.yml`
   file that checks out your repository and runs the unit tests inside the
   Docker image that you pushed to the DockerHub.

3. Push the `.github/workflows/test.yml` file to GitHub. Check that you get the
   green tick showing that your tests pass.

