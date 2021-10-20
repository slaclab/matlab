installing a containerized version of matlab

we use the iso install to do a completely install into a docker image. we use multipart builds and buildkit mounts in an attempt to minimise the container size.

get the iso from

https://www.mathworks.com/downloads/web_downloads/

get the file installation key from 

https://www.mathworks.com/licensecenter/licenses/40838630/6397849/activations

(difference license required?)

this assumes the network license - how best to not use that?


to install:

```
# mount the iso
make mount

# build
MATLAB_INSTALL_KEY=<blah> make build

# push to dockerhub
make push

# build a local singularity container
make singularity
```

running

by default, the images are stored under 

/sdf/sw/images/matlab//R2012a/matlab@R2012a.sif

you can instantiate matlab via

singularity exec -it /sdf/sw/images/matlab//R2012a/matlab@R2012a.sif matlab

