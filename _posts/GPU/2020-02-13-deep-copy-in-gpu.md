---
layout: post
title: Deep copy in GPU
categories: GPU
---
# Deep COPY
CUDA 6.0 이전에는 구조체를 HtoD 또는 DtoH 복사할 때, 단순히 구조체의 메모리 공간을 할당받고 데이터를 복사하는 것 뿐만 아니라 **참조하는 데이터의 주소값을 별도로 복사 해주는 작업** 이 필요하다.
```
struct dataElem {
    int prop1;
    int prop2;
    char * text;
}

void launch (dataElem * elem) {
    dataElem *g_elem;
    char *g_text;

    int textlen = strlen(elem->text);

    //Allocate storage for struct and text
    cudaMalloc(&g_elem, sizeof(dataElem));
    cudaMalloc(&g_text, textlen);  

    //copy each piece separately, including new "text" pointer value
    cudaMemcpy(g_elem, elem, sizeof(dataElem));
    cudaMemcpy(g_text, elem->text, textlen);
    cudaMemcpy(&(g_elem->text), &g_text, sizeof(g_text));

    //launch kernel, but host and device refereneces different memory space
    some_kernel<<...>>>(g_elem);
}
```
예시 코드의 경우 dataElem, text의 메모리를 할당하고 복사하는 것뿐만 아니라 추가로 주소를 복사하는 작업을 했다.
좀 더 복잡한 사례로 CPU와 GPU간 shared linked list를 복사하는 경우, 그나마 최적화하는 방법으로는 CPU쪽에 pinned memory를 사용하는 방식이 있다.
Unified memory는 host와 device간에 list element를 전달할 수 있고(사실상 주소 포인터를 넘기는 과정), host와 device 쪽 모두 list에 item을 삽입할 수 있다. (_물론 race condition이 없고, sync가 유지된다는 전제 하에_)

# Zero COPY
For memory allocation between host to device, there are two manners 1) non-mapped memory and 2) mapped, ponned memory(zero-copy).

## Mapped, pinned mempry (zero-copy) is useful under cricumstances,
+ The GPU has no meory on its own and uses RAM anyway
+ Data is load only once, but the computation to perform multiple and could hide the memory transfer latency
+ The host side wants to change/add more data or read the results, while kernel is stirll runnign
+ Data does not fit into GPU memory

_Or could use multiple stream and kernels to run in parallel._

## Pinned, but not mapped memory is useful
+ Data will be load and stored multiple time due to subsequent kernels or performing the work in steps.
+ Not much compatation to perform and loading latenciews are not going to be hidden


# reference
[SC13-Unified-Memory-CUDA](http://on-demand.gputechconf.com/supercomputing/2013/presentation/SC3120-Unified-Memory-CUDA-6.0.pdf)
[https://stackoverflow.com/questions/5209214/default-pinned-memory-vs-zero-copy-memory](https://stackoverflow.com/questions/5209214/default-pinned-memory-vs-zero-copy-memory)
