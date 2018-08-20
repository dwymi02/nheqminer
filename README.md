# nheqminer

This version of nheqminer is a continuation of the development effort, with the hope of making this a better ZEC mining tool.

* This version of nheqminer supports both CPU and GPU (NVIDIA CUDA) ZEC mining


<img src="https://github.com/dwymi02/nheqminer/blob/master/Starting%20nheqminer.png" width="619" >


#### Table of contents
* [Features](#features)
* [Download](#download)
* [Build](#build)
* [Runtime Dependencies](#dependencies)
* [Usage](#usage)
* [Donations](#donations)


## Features
* Decent performance
* Windows support for now, [provided by nicehash](https://github.com/nicehash/nheqminer/releases)
* Linux support (tested on Ubuntu 18.04 LTS)
* Stratum protocol support


## Download
* Binary releases: TBA
* Git tree: https://github.com/dwymi02/nheqminer.git
  * Clone with git clone https://github.com/dwymi02/nheqminer.git


## Build

### Dependencies
  - Boost 1.62+


## Windows

For the time being, Windows builds should be pulled from the original release, by NiceHash.
Available here: https://github.com/nicehash/nheqminer/releases

Download and install:
- [CUDA SDK](https://developer.nvidia.com/cuda-downloads) (if not needed remove **USE_CUDA_TROMP** and **USE_CUDA_DJEZO** from **nheqminer** Preprocessor definitions under Properties > C/C++ > Preprocessor)
- Visual Studio 2013 Community: https://www.visualstudio.com/en-us/news/releasenotes/vs2013-community-vs
- [Visual Studio Update 5](https://www.microsoft.com/en-us/download/details.aspx?id=48129) installed
- 64 bit version only

Open **nheqminer.sln** under **nheqminer/nheqminer.sln** and build. You will have to build ReleaseSSE2 cpu_tromp project first, then Release 7.5 cuda_tromp project, then select Release and build all.

### Enabled solvers
  - USE_CPU_TROMP
  - USE_CPU_XENONCAT
  - USE_CUDA_TROMP
  - USE_CUDA_DJEZO

If you don't want to build with all solvers you can go to **nheqminer Properties > C/C++ > Preprocessor > Preprocessor Definitions** and remove the solver you don't need.


## Linux
Working solvers CPU_TROMP, CPU_XENONCAT, CUDA_TROMP, CUDA_DJEZO

### Dependencies
  - CUDA -- 9.2
  - Boost -- 1.62 (built using 1.65.1)
  - build-essential -- 12.4
  - CMake -- 3.10.2

### General instructions
  - NVIDIA CUDA, refer to installation instructions via URL:
    http://developer.download.nvidia.com/compute/cuda/9.2/Prod/docs/sidebar/CUDA_Installation_Guide_Linux.pdf
    
  - The CUDA Toolkit can be downloaded from URL: https://developer.nvidia.com/cuda-downloads

  - Get the latest nheqminer repository:
    git clone https://github.com/dwymi02/nheqminer.git

  - Configure and build:
    * cd nheqminer/cpu_xenoncat/asm_linux
    * chmod +x fasm 
    * sh assemble.sh
    * cd ../../../
    * mkdir build && cd build
    * cmake -DCUDA_CUDART_LIBRARY="/usr/local/cuda-9.2/lib64/libcudart.so" ../nheqminer
    * make -j $(nproc)


## Dependencies

### Runtime Dependencies required to start nheqminer
  - NVIDIA CUDA toolkit.
  
    Please refer to the build section which provides the reference material for installing the NVIDIA CUDA toolkit

    For the time being the NVIDA CUDA toolkit is required even if you only wish to CPU mine ZEC coin.
    Development is working on providing a a CPU miner without the NVIDIA CUDA dependencies


## Usage

### Options

```
Parameters:
  -l [location] Stratum server:port
  -u [username] Username (wallet address)
  -a [port] Local API port (default: 0 = do not bind)
  -d [level]  Debug print level (0 = print all, 5 = fatal only, default: 2)
  -b [hashes] Run in benchmark mode (default: 200 iterations)
  -h    Print this help and quit

CPU settings
  -t [num_thrds]  Number of CPU threads
  -e [ext]  Force CPU ext (0 = SSE2, 1 = AVX, 2 = AVX2)

NVIDIA CUDA settings
  -ci   CUDA info
  -cd [devices] Enable CUDA mining on spec. devices
  -cb [blocks]  Number of blocks
  -ct [tpb] Number of threads per block
```

Example: -cd 0 2 -cb 12 16 -ct 64 128

When nheqminer is run without parameters, miner will utilize 75% of available logical CPU cores.

To see available parameters for nheqminer, from your command prompt enter the following command:

        nheqminer -h


Example to run benchmark on your CPU:

        nheqminer -b


Example to CPU mine, using your own wallet and worker id, on NiceHash USA server:

        nheqminer -l equihash.usa.nicehash.com:3357 -u YOUR_WALLET.YOUR_WORKER


Example to CPU mine, using your own wallet and worker id, on EU server, using 6 threads:

        nheqminer -l equihash.eu.nicehash.com:3357 -u YOUR_WALLET.YOUR_WORKER -t 6


Example to CPU mine, using your own wallet and worker id, on nanopool USA server:

        nheqminer -l zec-us-east1.nanopool.org:16666 -u YOUR_WALLET/YOUR_WORKER/YOUR_EMAIL@PROVIDER.com -p x -t [num_thrds]

Additional information about mining ZEC on nanopool please refer to https://zec.nanopool.org/help

Additional mining pools for your consideration available @ https://investoon.com/mining_pools/zec


<i>Note: if you have a 4-core CPU with hyper threading enabled (total 8 threads) it is best to run with only 6 threads (experimental benchmarks shows that best results are achieved with 75% threads utilized)</i>

Example to mine on your CPU as well on your CUDA GPUs with your own BTC address and worker1 on EU server, using 6 CPU threads and 2 CUDA GPUs:

        nheqminer -l equihash.eu.nicehash.com:3357 -u YOUR_WALLET.YOUR_WORKER -t 6 -cd 0 1


## Donations

### Donations are greatly appreciated and will be humbly accepted as reward for our labors ...

* BTC: `1HcQHQfhjmdTVBW6mYdsBP9esw3zns4S4u`
* ETH: `0xef5aa02df61f419d5bf0d75bd5cf6ff3a3d83269`
* ZEC: `t1PrZg5dBhcm7MfC21dcrRMxpD9tfzJiqAD`
* XMR: `46NX5s3K6ZX7cv4tF8C8moTUm3QpwNjjjarXfqUNsibxGc9aas6bSdmZCMDRgG9BWcPwoQrhJfGRCK6PAJTtBKT8Lpxct8F`
