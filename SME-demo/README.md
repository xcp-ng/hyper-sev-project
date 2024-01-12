# AMD SME Demonstrator

## Overview

This project demonstrates the usecase of AMD Secure memory Encryption (SME) technology. It includes a backend PV (paravirtualized) driver, frontend PV driver and user-level scripts to interact with the backend PV driver.

## Prerequisites

- AMD Processor with SME and SEV support
- Linux kernel 6.1.58 and Xen 4.18

## Installation

### Dom0:
- Install [Linux kernel](https://github.com/xcp-ng/linux/tree/sev_demo) and [Xen](https://github.com/xcp-ng/xen/tree/as-sme-demo) with our patches. Note that you'll need to run Xen in PVH mode for this demo to work. So make sure to add `dom0=PVH` in the Xen commandline and update the grub.
- Navigate to the backend driver: `linux/demo-sme/backend`
- Compile : `make` and load the backend PV driver: `insmod backend_pv.ko`

### DomU:
- Navigate to frontend driver:`linux/demo-sme/frontend`
- Compile the frontend driver : `make`
- You'll need to embed `frontend_pv.ko` in your initramfs/bzImage.
- Start the domU: `xl create -c pvh_guest.cfg`. Example of config can be found in this directory.
- Above command will take you to console of domU. Load frontend module: `insmod frontend_pv.ko`

### Usage:

- Get the dom_id from `xl list` and connect the drivers with `activate.sh <dom_id>`
- You should see proc entries under `/proc/sme`
- For testing you can write a text to `/proc/sme/sme_text` ane then set the encryption on with `echo "on" > /proc/sme/xenmem_encrypt`
- To set the encryption use `echo "off" > /proc/sme/xenmem_encrypt` (Note the garbage value in `xl dmesg` before encryption is set to off mode)

Note that this project is exclusively designed for demonstration purposes, illustrating the integration and utilization of AMD's Secure Memory Encryption (SME) technology in Linux+Xen environments.
For the production usage, upstream work in Xen will be followed. The details of the project phases can be found [here](https://lists.xenproject.org/archives/html/xen-devel/2023-10/msg02162.html).
