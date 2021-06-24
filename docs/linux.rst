linux notes
===========

linux installer shell maker
---------------------------
https://github.com/megastep/makeself

How to disable gui when ubuntu desktop version booting
----------------------------------------------------------
1. modify grub:
::

  sudo vim /etc/default/grub

change 
::

  GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"

to 

::

  GRUB_CMDLINE_LINUX_DEFAULT="text"

update grub
::

  sudo update-grub

2. disable lightdm service
::

  sudo systemctl disable lightdm.service

3. If you want to start desktop
::

  sudo servie lightdm start

4. To enable lightdm service, systemd has bug! ref: https://bugs.launchpad.net/ubuntu/+source/systemd/+bug/1595454
solution(root user or use sudo):
::

	systemctl enable lightdm
	ln -s /lib/systemd/system/lightdm.service /etc/systemd/system/display-manager.service

How to disable guest session
----------------------------
::

  sudo vim /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf

add:
::

  allow-guest=false


ubuntu 18.04 disable xorg using nvidia card!
--------------------------------------------
ref: https://askubuntu.com/questions/1061551/how-to-configure-igpu-for-xserver-and-nvidia-gpu-for-cuda-work

1. create file /etc/X11/xorg.conf with the following content:

::

  Section "Device"
    Identifier      "intel"
    Driver          "intel"
    BusId           "PCI:0:2:0"
  EndSection

  Section "Screen"
      Identifier      "intel"
      Device          "intel"
  EndSection


fix time difference in Ubuntu & Windows Dual Boot
--------------------------------------------------
Ubuntu use the hardware clock (RTC, real time clock) in universal time (UTC) by default 
while Windows use the clock in local time.

easy solution in ubuntu

.. code-block:: bash

  $ sudo timedatectl set-local-rtc 1





