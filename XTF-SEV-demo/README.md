# AMD SEV Demonstrator for the XTF guest

## Overview

This project demonstrates the usecase of AMD Secure Virtualization (SEV) technology in a XTF(Xen Testing Framework) guest. By running the XTF guest with SEV enabled, one can test how Xen handles protected guest memory and can confirm that the “guest secret” remains inaccessible to the XEN.

## Prerequisites

- AMD EPYC machines with SEV support

## Installation
- Install Xen and Xen-tools with our [patches](https://github.com/xcp-ng/xen/commits/hyper_sev_4.19/). Make sure to build the xen without enabling the `CONFIG_DEBUG` and `CONFIG_DEBUG_INFO`.
- Build XTF with our [patches](https://github.com/xcp-ng/xtf/commits/hyper_sev_xtf/)

## Usage
- Build XTF guest with `make`
- Execute this command: `./xtf-runner test-hvm64-sev`
- After the test completes, check the logs via `xl dmesg`. The test output should indicate whether Xen was able to read the guest's secret or not. illustrating the integration and utilization of AMD's Secure Encrypted Virtualization technology(SEV) in Linux+Xen environments. For the production usage, upstream work in Xen is in progress.



