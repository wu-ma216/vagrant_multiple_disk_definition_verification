# vagrant_multiple_disk_definition_verification

## Synopsis

This repository has a Vagrantfile defining one additional block device.  
You may learn how to write down vagrant definitions when you'd like to add a extra disk to your Vagrant VM.

## Background

I use and enjoy developments on Vagrant + Virtualbox in my job every day, and I know Vagrant provides disk addition function originally as of June 11 2022.  
However, that function isn't official but experimental. I may face not-available problems by later updates.  
So I'd like to realize one additional disk by using standard functions.

Instead of additional block devices, you can come up with using loopback devices.  
Of course I tried to use it, but I couldn't implement automatic losetup.  
I can carry out automatic mounts with loopback devices, but I want to use them as PVs or VGs in order to experiment LINSTOR at that time.

## Requirements for `vagrant up` with Vagrantfile in this repository

This indicates what version I've experimented creating the Vagrantfile.

- Windows 10 Home 21H2
- Vagrant 2.2.19
- Virtualbox 6.1.34 r150636 (Qt5.6.2)

## Reference

- https://sleeplessbeastie.eu/2021/05/10/how-to-define-multiple-disks-inside-vagrant-using-virtualbox-provider/
- https://github.com/hashicorp/vagrant/issues/9794#issuecomment-432121774
