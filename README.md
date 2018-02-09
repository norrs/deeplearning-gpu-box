# Deep learning GPU Docker environment

Tools and scripts for friends™ who trust eachother to share a GPU box to do GPU-development on for deep learning.

# Why this project?

Being able to run self-contained GPU development environments inside a
container to avoid having libraries fight each other due to Nvidia Driver <->
Cuda Toolkit <-> cuDNN (CUDA Deep Learning Neural Network library) together
with Python2( why would you?!) and Python 3, and not at least different
versions of Tensorflow having different requirements... to say the least, it's
a huge dependency list to maintain. Running GPU-dev inside a container where
you can contain everything beside the Nvidia driver, simplifies your life and
avoids screwing up your HOST OS. 

You had to use a sad library which only works on a particular tensorflow
version? Not a problem, run the container with correct dependencies which pulls
in exactly the given version of cuDNN and Cuda Toolkit!

Since I personally prefer to run stuff as non-root, and this also doesn't screw up
with file ownership when mounting my own $HOME directory from the HOST inside the container, these are helper scripts helping you to exactly do that.


## Alternatives 

A more simple route is using [igorbb](https://github.com/igorbb)'s [gpu-dev](https://hub.docker.com/r/igorbb/gpu-dev) directly, if you don't mind running everything as root inside the container. 

# Install

TODO: Write docks :-))))))

# Usage

TODO: Fix even better usage; for now:

```
dz-build [image_directory=$USER/gpu-dev] (looks for folders in ~/images/ !)
dz-run <gpu_id (0|1> [port=8888] [image=$USER/gpu-dev] [cmd=/usr/local/bin/jupyter notebook --no-browser --ip=0.0.0.0]
dz-run 1 9999   # Is usually enough
dz-shell-root # gains root shell in your container run from dz-run

Current usage shown by dz-usage ↓↓↓:
 If above ↑↑↑ empty, no users running containers using GPU


Remember to stop/kill your container after usage! Make sure you save notebook first!
 Kill container by executing «docker stop $USER»

This help text from dz-help
```


# Credits

[igorbb](https://github.com/igorbb) for the initial concept of getting it to run inside Docker and sharing his gpu-dev image https://hub.docker.com/r/igorbb/gpu-dev/
