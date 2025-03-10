---
# You can also start simply with 'default'
theme: dracula
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://access-ci.org/wp-content/uploads/2025/02/Turbulence-1536x864.jpg
# some information about your slides (markdown enabled)
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
