# DPDK burst replay tool

## Introduction

The tool is designed to provide high DPDK performances to burst any pcap dump on
a single or multiple NIC port(s).

To do so, the pcap files will be cached on hugepages before being sent through DPDK.

## How to play with it

### Install dependencies

* dpdk-dev (obsly)
* libnuma-dev
* That's all.

NB: libpcap is not required, as dpdk-replay process pcap files manually.

### Compiling and installing it

```bash
mkdir build
cd build
cmake ..
make
sudo make install
```

### Launching it

```bash
dpdk-replay [--nbruns NB] [--numacore 0|1] FILE NIC_ADDR[,NIC_ADDR...]
```

Example:
```bash
dpdk-replay --nbruns 1000 --numacore 0 foobar.pcap 04:00.0,04:00.1,04:00.2,04:00.3
```

## TODO

* Add a configuration file or cmdline options for all code defines.
* Add an option to configure maximum bitrate.
* Add an option to send the pcap with the good pcap timers.
* Add an option to send the pcap with a multiplicative speed (like, ten times the normal speed).
* Add an option to select multiple pcap files at once.
* Be able to send dumps simultaneously on both numacores.
* Split big pkts into multiple mbufs.
* Add a Python module to facilitate scripting (something like what does scapy for tcpreplay sendpfast func).
* Manage systems with more than 2 numa cores.
* Use the maximum NICs capabilities (Tx queues/descriptors).

## BSD LICENCE

Copyright 2018 Jonathan Ribas, FraudBuster. All rights reserved.
