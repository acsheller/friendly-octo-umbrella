# friendly-octo-umbrella

This is a project that containerizes SCADS [SUBER](https://github.com/giorgiopiatti/SUBER) It is based on the paper `An LLM-based Recommender System Environment`. Some key steps in setting up the project are provided. 

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
docker run --gpus all -it -v /path/to/local/directory:/home/suber/SUBER:rw --name suber-container suber-con
```
https://github.com/giorgiopiatti/SUBER.git
### At the Prompt

type a few commands such as

```.bash
nvidia-smi
```

TODO Need to setup a command for Jupyter-lab to run or setup the instructions here.

## Follow git Repository Examples

Begin by ensuring the container launches and that `nvidia-smi` returns a GPU.  

```.bash
(MPR) suber@550c6d819038:~/SUBER$ nvidia-smi
Wed Jun 12 14:07:14 2024       
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 545.29.06              Driver Version: 545.29.06    CUDA Version: 12.3     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA A10G                    Off | 00000000:00:1E.0 Off |                    0 |
|  0%   26C    P8               9W / 300W |      4MiB / 23028MiB |      0%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+
                                                                                         
+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|  No running processes found                                                           |
+---------------------------------------------------------------------------------------+
(MPR) suber@550c6d819038:~/SUBER$ 
```

### ablations

I'm not sure what to pass in as arguments so need to figure that out. 

```.python
python3 -m ablations.movies.run <args>
```





## References

1. "An LLM-based Recommender System Environment" by Nathan Coreco*, Giorgio Piatti*, Luca A. Lanzendörfer, Flint Xiaofeng Fan, Roger Wattenhofer.
