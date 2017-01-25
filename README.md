# Docker FET images for Continous Integration

Current distributions available:

* CentOS 7
* Debian 8
* OpenSuse 42.2
* Ubuntu 16.04

# Building images

Run:

```
./manage_images -h
```

# Running the images

To run, for example, the CentOS7 image:

```
docker run -t --name test juliogonzalez/centos7-fetdev
```
