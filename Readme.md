# SCADS SUBER CONTAINER

## Build the container

This can take a very long time, about 30 minutes to build initially.  The order in which the "runs" are done is important because each creates a layer that will either get rebuilt causing more time to be spent or will be passed over. This can be optimized such that it does not take that long.

It is also pretty large ~28GB, however, having it containerized means that changes impact the container and not the system it is running on.

```.bash
docker build -t suber-con .
````

## Run the container without mounting in a volume

Source code is cloned into the repository and is already there so no need to mount it in for an initial trial.

```.bash
docker run --gpus all -it  --name suber-container suber-con
```

## Run the container with a volume mounted in

This will mount in `/path/to/local/directory` to inside of the container at `/home/suber/SUBER`.  Do this if you have `git cloned` the repository and are making changes to source code.  For example if you are adding a `MIND` dataset to it -- *Note the repo does show the general approach for adding new datatypes other than movies or books* -- then one will need to add the `environment`, `algorithms`, and etc.

```.bash
docker run --gpus all -it -v /path/to/local/directory:/home/suber/SUBER --name suber-container suber-con
```

### At the Prompt

type a few commands such as

```.bash
nvidia-smi
```

TODO Need to setup a command for Jupyter-lab to run or setup the instructions here.

## Follow git Repository Examples

Begin by
