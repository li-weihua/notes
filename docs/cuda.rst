###############
cuda related
###############

***************************************
how to install nvidia driver in linux?
***************************************

Problem: NVIDIA kernel module 'nvidia-drm' already be loaded in kernel

Solution (in root):

#. goto true tty3, pressing ``Ctrl+Alt+F2``

#. disable the graphical target::

    systemctl isolate multi-user.target

#. unload the Nvidia drivers::
   
    modprobe -r nvidia-drm

#. install cuda driver

#. start the GUI again::

    systemctl start graphical.target

#. confirm your driver version::

    nvidia-smi

***********************
download nvidia driver
***********************

website: https://www.nvidia.com/Download/Find.aspx



