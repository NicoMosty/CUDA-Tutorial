---
clicks: 2
---

# How Does CUDA Actually Work?

<div v-click="[0]">
<div style="position: absolute; top:20%; left: 5%; width: 90%; text-align: center;">

CUDA is far more than a single entity—it's a comprehensive, multi-layered platform that integrates a wide array of technologies, software libraries, and low-level optimizations, collectively creating a robust parallel computing ecosystem. At its core, CUDA allows developers to harness the full power of NVIDIA GPUs, enabling massive parallelism that accelerates computations far beyond what a CPU alone can achieve.

</div>

<div style="position: absolute; top:50%; left: 1%">
<Youtube id="-P28LKWTzrI?start=15" width="450" height="250" />
</div>

<div style="position: absolute; top:50%; left: 50%">
<Youtube id="-P28LKWTzrI?start=71" width="450" height="250" />
</div>

</div>

<!-- ======================================================================================== -->

<div v-click="[1]">

<div class="absolute left-1/10 w-1/3" style="text-align: center;">

**Low-level**:  Parallel programming model that lets developers tap into the raw power of GPUs using a C++-like syntax.

</div>

<Arrow x1="420" y1="150" x2="550" y2="150" />

<div style="position: absolute; top: 10%; left: 55%;">

<img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Nvidia_CUDA_Logo.jpg" alt="Nvidia CUDA Logo" style="position: absolute; top:25%; left: 65%; width: 25%;"/>
<img src="https://i.blogs.es/9777ce/chip/1366_2000.jpg" style="position: absolute; top:55%; left: 65%; width: 25%;"/>

```mermaid {scale: 0.9}
graph TB
    A[CPU] -->|Sends CUDA code| B[CUDA]
    B -->|Executes in parallel| C[GPU]
    C -->|Processes tasks in parallel| D[Results]
    
    %% Add images to enhance the nodes
    classDef cpuStyle fill:#f2f2f2,stroke:#000000,stroke-width:2px;
    classDef cudaStyle fill:#ffffcc,stroke:#000000,stroke-width:2px;
    classDef gpuStyle fill:#e0f7fa,stroke:#000000,stroke-width:2px;

    class A cpuStyle;
    class B cudaStyle;
    class C gpuStyle;

    A -->|"CPU sends CUDA code"| B
    B -->|"Parallel tasks executed on GPU"| C
    C -->|"GPU processes tasks concurrently"| D

```

</div></div>


<!-- ======================================================================================== -->

<div v-click="[2]">

<div class="absolute top-1/3 left-1/10 w-1/3" style="text-align: center;">

**Complex set of libraries and frameworks—middleware** that supports critical vertical use cases, such as AI, with tools like cuDNN for PyTorch and TensorFlow.

**Suite of high-level solutions**: Such as TensorRT-LLM and Triton, which simplify AI workloads like LLM serving, allowing users to leverage CUDA’s power without needing deep expertise in the platform itself.

</div>

<Arrow x1="420" y1="330" x2="550" y2="330" />

<div style="position: absolute; top: 10%; left: 55%;">

<img src="https://miro.medium.com/v2/resize:fit:691/1*VSQ0XEywxSgZBwW05GsZtw.png" alt="Nvidia CUDA Logo" style="position: absolute; top:0%; left: 75%; width: 25%;"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Nvidia_CUDA_Logo.jpg" alt="Nvidia CUDA Logo" style="position: absolute; top:29%; left: 65%; width: 25%;"/>
<img src="https://i.blogs.es/9777ce/chip/1366_2000.jpg" style="position: absolute; top:55%; left: 65%; width: 25%;"/>

```mermaid {scale: 0.9}
graph TB
    A[TensorFlow/PyTorch] -->|Uses CUDA libraries| B[CUDA]
    B -->|Performs parallel computations| C[GPU]
    C -->|Accelerates deep learning tasks| D[Results]
    
    %% Add images to enhance the nodes
    classDef tfStyle fill:#e1f5fe,stroke:#000000,stroke-width:2px;
    classDef cudaStyle fill:#ffffcc,stroke:#000000,stroke-width:2px;
    classDef gpuStyle fill:#e0f7fa,stroke:#000000,stroke-width:2px;

    class A tfStyle;
    class B cudaStyle;
    class C gpuStyle;

    A -->|"TensorFlow or PyTorch sends computations"| B
    B -->|"Parallel computations on GPU"| C
    C -->|"GPU accelerates deep learning tasks"| D


```

</div></div>

---
level: 2
clicks: 2
---

<h1>How Does CUDA Actually Work?</h1>

## CPU vs. GPU: Key Differences
<img v-click="[0]" src="https://enccs.github.io/gpu-programming/_images/CPUAndGPU.png" style="position: absolute; top:25%; left: 15%; width: 70%;"/>

<img v-click="[1]" src="https://enccs.github.io/gpu-programming/_images/CPUAndGPU.png" style="position: absolute; top: 25%; left: 15%; width: 70%; clip-path: inset(0 65% 0 0);"/>

<div v-click="[1]">
<div style="position: absolute; top: 30%; left: 55%; width: 40%; text-align: left; font-size: 1.2em;">

CPUs were designed to excel at executing a sequence of operations, called a thread, as fast as possible. They can execute a few tens of these threads in parallel. CPUs rely on large data caches and complex flow control to avoid long memory access latencies.
</div></div>

<img v-click="[2]" src="https://enccs.github.io/gpu-programming/_images/CPUAndGPU.png" style="position: absolute; top: 25%; left: 15%; width: 70%; clip-path: inset(0 0 0 65%);"/>

<div v-click="[2]">
<div style="position: absolute; top: 30%; left: 10%; width: 40%; text-align: left; font-size: 1.2em;">

GPUs were designed to excel at executing many thousands of threads in parallel. They were originally developed for the highly-parallel task of graphic processing, prioritizing data processing over data caching and flow control. This design allows the GPU to hide memory access latencies with computation, instead of using large caches and complex flow control.
</div></div>

