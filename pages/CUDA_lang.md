---
clicks: 3
---

# So, How Do You Write CUDA Code Anyway?

<h2>CPUs problem</h2>

<div style="width: 40%;">
```python
# Function to compute Y = W * X + B
def linear_layer(X, Y, N, n):
    X = [0] * n
    for i in range(n):
        X[i] = Y[i] * N[i] + B[i]
    return Y
```
</div>

<div style="position: absolute; left: 50%; top: 22%; width: 40%;">
Parallelization on CPUs typically involves threads that execute instructions independently. For example, a for-loop performing operations on arrays can be parallelized by assigning each iteration to a separate thread.
</div>

<blockquote v-click="[1]" style="position: relative; top: 1%;">
  😓 But it iterates over the elements of the arrays one by one, computes the individual result, and stores it in the output array.
</blockquote>

<!-- ================================== -->
<div style="position: relative;left: -2%; top: 15%;width: 40%;">

$$ {hide|1|2}{at:'2'}
Independent=
\begin{cases}
X[i] &= W[i] + B[i] \\ 
X[j] &= W[j] + B[j] 
\end{cases}
$$
</div>

<p v-click="[3]" style="position: relative; left: 50%; top: -10%; width: 55%;">
Modern CPUs are limited in parallelism due to having a limited number of cores (usually no more than 16). While GPUs can handle multiple threads with multi-threading, deep learning tasks, which involve large vectors and matrices, benefit from GPUs. GPUs can execute millions of threads in parallel, vastly improving performance for these computation-heavy operations.
</p>

---
clicks: 1
level: 2
---

<h1>So, How Do You Write CUDA Code Anyway?</h1>

<div v-click="[0, 2]">

## Terminology
</div>

<div v-click="[0]">

- **Host**: Refers to the CPU and its memory.
- **Device**: Refers to the GPU and its memory.
</div>

<div v-click="[1]"  style="position: absolute; top: 25%; width: 40%;">

- **Host Code**: Code that runs on the CPU.
- **Device Code**: Code that runs on the GPU.
- **Host Memory**: Memory accessible by the CPU.
- **Device Memory**: Memory accessible by the GPU.
- **Host-to-Device Transfer**: Copying data from the host memory to the device memory.
- **Device-to-Host Transfer**: Copying data from the device memory to the host memory.
</div>

<div v-click="[0]" style="position: absolute; top: 40%; left: 20%; width: 100%; text-align: center;">

<img src="https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdec9a939-cd30-4fd8-b17c-4efb0473a6da_700x292.png" alt="Nvidia CUDA Logo" />

</div>



<div v-click="[1]">

<div style="position: absolute; top: 20%; left: 50%; width: 40%; text-align: center;">

<img src="https://postfiles.pstatic.net/MjAxNzA5MjZfMjYg/MDAxNTA2NDE0MzQyMDgw.Vu6hG-1O-GpEPEyl6wE73S15gMwgdMJU_4zHxTTlIFMg.W9qHd53DgF1I87MxE6ZOeDGC8w_TtMJuDWE1kAVJrLsg.PNG.n_cloudplatform/2.png?type=w3840"/>
</div>

<svg style="position: absolute; top: 19%; left: 49%; width: 100%;">
  <rect width="410" height="750" style="fill: none; stroke: red; stroke-width: 2"/>
</svg>

<svg style="position: absolute; top: 41%; left: 49%; width: 100%;">
  <rect width="410" height="750" style="fill: none; stroke: red; stroke-width: 2"/>
</svg>

[HOST]{style="position: absolute; top: 15%; left: 50%; width: 40%;font-size: 20px;; color: red"}
[DEVICE]{style="position: absolute; top: 41%; left: 82%; width: 40%;font-size: 20px;; color: red"}

</div>

---
level: 2
clicks: 11
---

<h1>So, How Do You Write CUDA Code Anyway?</h1>

## Execution Workflow
  
<div  v-click="[0,3]" style="position: absolute; top: 25%; left: 5%; width: 50%; border: 1px solid #ccc; padding: 5px; text-align: center;">
    <h3>Preparation on the host</h3>
    The host CPU executes the main part of the CUDA program, setting up data in its own memory, and preparing instructions.
</div>

<div  v-click="[3,6]" style="position: absolute; top: 25%; left: 5%; width: 50%; border: 1px solid #ccc; padding: 5px; text-align: center;">
    <h3>Data transfer</h3>
    Before the GPU can begin processing, the necessary data must be transferred from the host’s memory to the device’s memory.
</div>

<div  v-click="[6,8]" style="position: absolute; top: 25%; left: 5%; width: 50%; border: 1px solid #ccc; padding: 5px; text-align: center;">
    <h3>Kernel launch</h3>
    The host directs the device to execute a kernel, and the GPU schedules and runs the kernel across its many threads
</div>

<div v-click="[8,12]" style="position: absolute; top: 25%; left: 5%; width: 50%; border: 1px solid #ccc; padding: 5px; text-align: center;">
    <h3>Post-processing</h3>
    After the GPU has finished executing the kernel, the results are typically transferred back to the host for further processing or output, completing the compute cycle.
</div>

<div style="position: absolute; top: 47%; left: 5%; width: 50%;">

```cpp {none|1-2|4-7|hide}{at:'1'}
// Allocate memory on host
float *h_A = (float*)malloc(N * sizeof(float));

// Initialize the data
for (int i = 0; i < N; i++) {
    h_A[i] = (float)i;
}
```
</div>


<div style="position: absolute; top: 47%; left: 5%; width: 50%;">
```cpp {hide|none|1-2|4-8|hide}{at:'3'}
// Allocate memory on the device
cudaMalloc((void**)&deviceData, sizeof(int));

// Transfer data from host to device
cudaMemcpy(
    deviceData, &hostData, sizeof(int), 
    cudaMemcpyHostToDevice
);
```
</div>

<div style="position: absolute; top: 47%; left: 5%; width: 50%;">
```cpp {hide|none|1-2|hide}{at:'6'}
// Launch the kernel with 10 threads (1 block, 10 threads)
kernelExample<<<1, 10>>>(deviceData);
```
</div>

<div style="position: absolute; top: 47%; left: 5%; width: 50%;">
```cpp {hide|none|1-5|7-12|13-14|hide}{at:'8'}
    // Copy the result back from device to host
    cudaMemcpy(
        hostData, deviceData, 10 * sizeof(int), 
        cudaMemcpyDeviceToHost
    );

    // Print the results
    for (int i = 0; i < 10; ++i) {
        std::cout << "Value at index " << i << ": " << hostData[i] 
                  << std::endl;
    }

    // Clean up
    delete[] hostData; cudaFree(deviceData);
```
</div>




---
level: 2
clicks: 3
---

<h1>So, How Do You Write CUDA Code Anyway?</h1>

## CUDA Kennels

<img v-click="[0]"  src="../images/cuda-kernel/thread.svg" style="position: absolute; top: 40%; left: 0%; width: 40%; text-align: center;">

<img v-click="[0]"  src="../images/cuda-kernel/block.svg" style="position: absolute; top: 30%; left: 45%; width: 50%; text-align: center;">

<Arrow v-click="[0]" x1="340" y1="350" x2="420" y2="350" />

<!-- ===================================================================== -->

<img v-click="[1]"  src="../images/cuda-kernel/block.svg" style="position: absolute; top: 40%; left: 2%; width: 40%; text-align: center;">

<img v-click="[1]"  src="../images/cuda-kernel/grid.svg" style="position: absolute; top: 20%; left: 45%; width: 45%; text-align: center;">

<Arrow v-click="[1]" x1="340" y1="400" x2="420" y2="400" />

<!-- ===================================================================== -->

<img v-click="[2]"  src="https://www.dailydoseofds.com/content/images/size/w1000/2024/05/image-22.png" style="position: absolute; top: 25%; left: 2%; width: 50%; text-align: center;">

<img v-click="[2]"  src="https://www.dailydoseofds.com/content/images/size/w1000/2024/05/image-24.png" style="position: absolute; top: 65%; left: 45%; width: 50%; text-align: center;">

<Arrow v-click="[2]" x1="300" y1="300" x2="420" y2="400" />

<!-- ===================================================================== -->
<img v-click="[3]"  src="../images/cuda-kernel/CUDA_domain.svg" style="position: absolute; top: 25%; left: 25%; width: 50%; text-align: center;">

---

# PENDING

[Page 17 -> CUDA C/C++ BASICS | NVIDIA CORP](https://researchcomputing.princeton.edu/sites/g/files/toruqf7036/files/documents/01_Introduction_to_CUDA_C_short_rmc_v1_hackathon.pdf)