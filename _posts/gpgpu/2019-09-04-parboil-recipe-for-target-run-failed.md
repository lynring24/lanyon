---
layout: post
title: parboil recipe for target 'run' failed
categories: gpgpu
tags: [cuda, parboil, gpgpu, benchmark]
---

벤치마크 Parboil을 설치하는 대신 **환경변수** 때문에 삽질을 했다.
> USER_PATH = 사용자 HOME 디렉터리

```
$ ./parboil run cutcp cuda small
Parboil parallel benchmark suite, version 0.2

/usr/local/cuda/bin/nvcc -O2  -I/USER_PATH/benchmark/Parboil/common/include -I/usr/local/cuda-8.0/include  -c /USER_PATH/benchmark/Parboil/common/src/parboil_cuda.c -o build/cuda_default/parboil_cuda.o
nvcc warning : The 'compute_20', 'sm_20', and 'sm_21' architectures are deprecated, and may be removed in a future release (Use -Wno-deprecated-gpu-targets to suppress warning).
/USER_PATH/benchmark/Parboil/common/src/parboil_cuda.c: In function ‘pb_AddSubTimer’:
/USER_PATH/benchmark/Parboil/common/src/parboil_cuda.c:351:28: warning: embedded ‘\0’ in format [-Wformat-contains-nul]
   sprintf(subtimer->label, "%s\0", label);
                            ^
gcc -O2  -I/USER_PATH/benchmark/Parboil/common/include -I/usr/local/cuda-8.0/include  -c /USER_PATH/benchmark/Parboil/common/src/args.c -o build/cuda_default/args.o
/usr/local/cuda/bin/nvcc -o build/cuda_default/cutcp -L/usr/local/cuda-8.0/lib64 -lm -lpthread -lm build/cuda_default/main.o build/cuda_default/readatom.o build/cuda_default/output.o build/cuda_default/excl.o build/cuda_default/cutcpu.o build/cuda_default/cutoff6overlap.o build/cuda_default/parboil_cuda.o build/cuda_default/args.o
nvcc warning : The 'compute_20', 'sm_20', and 'sm_21' architectures are deprecated, and may be removed in a future release (Use -Wno-deprecated-gpu-targets to suppress warning).
Resolving CUDA runtime library...
/USER_PATH/benchmark/Parboil/common/mk/cuda.mk:90: recipe for target 'run' failed
make: *** [run] Error 1
Run failed!
```

#### 문제
<pre>
cuda makefile에서 환경변수 문제가 있었다.
@$(shell echo $(RUNTIME_ENV)) LD_LIBRARY_PATH=$(CUDA_LIB_PATH) ldd $(BIN) | grep cuda
문제가 되는 환경 변수 RUNTIME_ENV는 지웠다.
</pre>


## 수정한 파일

#### parboil/common/mk/cuda.mk
```
 89 run:
 90     @echo "Resolving CUDA runtime library..."
 91 #   original code : checking the dependancy 
 92 #   @$(shell echo $(RUNTIME_ENV)) LD_LIBRARY_PATH=$(CUDA_LIB_PATH) ldd $(BIN) | grep cuda
 93 #   @$(shell echo $(RUNTIME_ENV)) LD_LIBRARY_PATH=$(CUDA_LIB_PATH) $(BIN) $(ARGS)
 94 #   modified code
 96     @LD_LIBRARY_PATH=$(CUDA_LIB_PATH) $(BIN) $(ARGS)

```
#### parboil/common/Makefile.conf

```
OPTIMIZATION=2
CUDA_PATH=/usr/local/cuda
CUDA_LIB_PATH=/usr/local/cuda/lib64
OPENCL_PATH=/usr/local/cuda
OPENCL_LIB_PATH=/usr/lib
```

## Result
```
Resolving CUDA runtime library...
read 5943 atoms from file '/home/dcslab/hrchung/benchmark/Parboil/datasets/cutcp/small/input/watbox.sl40.pqr'
extent of domain is:
  minimum -19.998 -19.941 -19.961
  maximum 19.974 20 19.974
padding domain by 0.5 Angstroms
domain lengths are 40.972 by 40.941 by 40.935
Invoking CUDA kernel on 11 region planes...
computing extra atoms on CPU

Finished CUDA kernel calls

IO        : 0.017945
Kernel    : 0.003808
Copy      : 1.605655
Driver    : 0.000184
Compute   : 0.048384
CPU/Kernel Overlap: 0.003808
Timer Wall Time: 1.672222
Pass
```
