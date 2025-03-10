---
favicon: https://img.icons8.com/external-filled-line-andi-nur-abdillah/64/external-GPU-gaming-(filled-line)-filled-line-andi-nur-abdillah.png
background: https://images.unsplash.com/photo-1624421514201-db391243ed51?q=80&w=2428&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

backgroundSource: unsplash 
backgroundSourceUrl: https://images.unsplash.com/photo-1624421514201-db391243ed51?q=80&w=2428&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

date: 10/03/2025

# You can also start simply with 'default'
theme: dracula

title: Introducción a CUDA
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  enabled: true
  # persist: true
  syncAll: true
  
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true

addons:
  - excalidraw

hideInToc: true
---

# CUDA 101
Unlocking Parallel Computing with GPUs

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Let's Start <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/NicoMosty/CUDA-Tutorial" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
hideInToc: true
---

# TOC
<Toc maxDepth="3" />


---
src: ./pages/intro.md
---

---
src: ./pages/CUDA.md
---

---
src: ./pages/history.md
---

---
src: ./pages/CUDA_lang.md
---
