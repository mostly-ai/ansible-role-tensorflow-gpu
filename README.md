ansible-role-tensorflow-gpu
=========

Installs the requirements for the `tensorflow-gpu` Python package (by default for version `2.0`). It doesn't install 
either either Python or the `tensorflow-gpu` package. 

Tested with Tesla K80, Ubuntu 18.04, Nvidia drivers 418, CUDA 10.0, NCCL 2.5, CUDNN 7.6 and Tensor RT 6.0.

Optionally also installs nvidia_init which initializes the GPUs during boot.

Requirements
------------

Outbound access to http://developer.download.nvidia.com/compute/cuda/repos/

Role Variables
--------------

    gpu: false
    nvidia_driver_version: "418.87.01"
    cuda_version: "10.0.130"
    nccl_version: "2.5.6"
    cudnn_version: "7.6.5.32"
    tensor_rt_version: "6.0.1"
    nvidia_restart_node_on_install: true
    nvidia_init: true
    nvidia_bash_profile: true

- `gpu`: `true` is needed. Without it this role does nothing.
- `nvidia_driver_version`: Nvidia driver version to install
- `cuda_version`: Nvida CUDA version to install
- `nccl_version`: Nvidia NCCL version to install
- `cudnn_version`: Nvidia CUDNN version to install
- `tensor_rt_version`: Nvidia Tensor RT version to install
- `nvidia_init`: Installs a bash script that is executed via systemd
- `nvidia_gpu_name0`: `/dev/nvidia0` - set this to the device ansible looks for. If it does not exist then if 
`nvidia_init` is `true` then it will run the `nvidia_init.sh` script
- `nvidia_restart_node_on_install`: restarts the system when packages are installed or updated


Example Playbook
----------------

`playbook.yml`:

    - hosts: deep_learning
      roles:
        - mostly-ai.tensorflow-gpu

`inventory`:

    [deep_learning]
    host1.example gpu=true

Example Errors
--------------

This error means you are not using a supported OS (like Ubuntu 18.10 which does not have Nvidia URLs)
<pre>
   "msg": "No file was found when using with_first_found. Use the 'skip: true' option to allow this task to be skipped 
   if no files are found"
</pre>

Tests in playbook
----------------

They are using this one: https://github.com/lae/ansible-role-travis-lxc

License
-------

MIT

Author Information
------------------

