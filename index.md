---
marp: true
theme: default  
paginate: true
header: ![height:40px](https://quantstack.net/img/logo.svg)
footer: ![height:20px](img/twitter.svg) ![height:20px](img/github.svg) @JohanMabille @ThorstenBeier @QuantStack
style: @import url('https://unpkg.com/tailwindcss@^2/dist/utilities.min.css');
---
<style>
section::after {
  content: attr(data-marpit-pagination) '/' attr(data-marpit-pagination-total);
}
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>


![bg fit right:30%](https://jupyter.org/assets/homepage/main-logo.svg)

# xeus kernels in the browser

## JupyterCon 2023

---

# About

<div class="grid grid-cols-2 gap-4">
<div>

## Johan Mabille

- Technical Director at QuantStack
- Jupyter Distinguished Contributor
- Co-authored the xeus stack, the debugger in Jupyter
- Leads the development of mamba

</div>
<div>

## Thorsten Beier

- Scientific Software Developer at QuantStack
- Co-authored the emscripten-forge stack
- Contributor to many open-source projects 

</div>
</div>

---

# Jupyter architecture

![h:400px center](https://xeus.readthedocs.io/en/latest/_images/jupyter_archi.svg)

- A well-specified protocol built upon web standards
- Implemented for more than 40 languages

---

# The Jupyter kernel protocol

Clients and kernels communicate (over the network) through 5 channels:
- Shell: code execution, code completion
- Control: stop and restart, kernel info, debugging
- stdin: input request
- IOPub: broadcast channel to publish results and kernel state
- Heartbeat: to check the kernel is still alive

ZeroMQ provides the low-level transport layer over which the messages are sent.


---

# Writing kernels for Jupyter

- Write from scratch in your favorite language
- Adopt the kernel wrapper approach, based on ipykernel
- Build upon xeus, a native implementation of the protocol

---

# Xeus

- xeus is a C++ library which simplifies the implementation of kernels for Jupyter
- developers can focus on implementing the interpreter part of the kernel
- Tutorial for creating a kernel based on xeus: https://xeus.readthedocs.io/en/latest/kernel_implementation.html
- xeus is architected in components that can be replaced with ad-hoc implementations

--- 

# The Xeus Universe


<div class="grid grid-cols-3 gap-4">

  <div>

  ![height:115px](img/xeus-python-logo.svg) ![height:115px](img/python_gif.gif)
  ![height:115px](img/xeus-sql-logo.svg) ![height:115px](img/xeus-sql-screencast.gif)
  </div>
  <div>

  ![height:115px](img/xeus-cling.svg) ![height:115px](img/xeus-cling-screenshot.png)
  ![height:115px](img/xeus-sqlite-logo.svg) ![height:115px](img/xeus-sqlite-screenshot.png)


  </div>
  <div>

  ![height:115px](img/xeus-lua-logo.svg)  ![height:115px](img/lua.gif)
  ![height:115px](img/xeus-robot.svg) ![height:115px](img/robo_gif.gif)
  
  </div>

</div>

---

# The Xeus Universe


<div class="grid grid-cols-3 gap-4">

  <div>

  ![height:115px](img/xeus-octave-logo.svg) ![height:115px](img/native-octave-plots.png)
  ![height:115px](img/xeus-qt-logo.svg) ![height:115px](img/xeus-qt-gif.gif)

  </div>
  <div>

  ![height:115px](img/xeus-nelson-logo.svg) ![height:115px](img/nelson.png)
  ![height:115px](img/3DSlicerLogo-HorizontalF.svg) ![height:115px](img/youtube-video-gif.gif)
   
  </div>
  <div>

  ![height:115px](img/xeus-wren-logo.svg) ![height:115px](img/wren_gif.gif)
  ![height:115px](img/xeus-cookiecutter.svg) <br> ![height:115px](img/usage.gif)

  
  </div>

</div>



<!-- 
---


# The xeus galaxy



- xeus: a native implementation of the Jupyter Kernel Protocol
- xeus + interpreter + glue code = Jupyter kernel
- xeus-cling (C++), xeus-python, xeus-sql, xeus-lua, etc...
- xwidgets: a native backend for the Jupyter interactive widgets -->

---

# Implementing a kernel

<style scoped>
{
   font-size: 1.5rem;
}
</style>

* Start from a cookiecutter template:


```
cookiecutter https://github.com/jupyter-xeus/xeus-cookiecutter
```


* Implement a handfull of methods:
  * execute request
  * complete request
  * inspect request
  * ...

![bg fit right](img/echo-kernel.png)






---

# Traditional usage of Jupyter Kernels

![h:500px center](img/zmq_piecewise/zmq5.svg)


---

# Traditional usage of Jupyter Kernels

![h:500px center](img/zmq_piecewise/zmq4.svg)


---

# Traditional usage of Jupyter Kernels

![h:500px center](img/zmq_piecewise/zmq3.svg)

--- 

# Traditional usage of Jupyter Kernels

![h:500px center](img/zmq_piecewise/zmq2.svg)


---

# Traditional usage of Jupyter Kernels

![h:500px center](img/zmq_piecewise/zmq1.svg)


---

# Traditional usage of Jupyter Kernels

![h:500px center](img/zmq_piecewise/zmq0.svg)


---

![h:300 center](img/webassembly-ar21.svg)

* Wasm is a binary instruction format for a stack-based virtual machine
* Portable compilation target for programming languages
* Enabling deployment on the web

---
# Emscripten
![h:200 center](img/emscripten_logo.svg)


### Emscripten is a complete compiler toolchain to WebAssembly, using LLVM, with a special focus on speed, size, and the Web platform.

---


# WebAssembly allows to run native code in the browser.

<style scoped>
{
   font-size: 1.4rem;
}
</style>

<!-- <div class="grid grid-cols-2 gap-4"> -->

<!-- A 2X2 GRID -->
<div class="grid grid-cols-2 grid-auto-rows gap-4">

<div>

  Doom:
  ![width:34px](img/github-mark.svg) [github.com/cloudflare/doom-wasm](https://github.com/cloudflare/doom-wasm)
  ![height:150px](img/doom.gif)

</div>

<div>

  x86 emulator:  
  ![width:34px](img/github-mark.svg) [https://github.com/copy/v86](https://https://github.com/copy/v86)
  ![height:150px](img/Windows2000_desktop.png)

</div>
<div>

  Python:
  ![width:34px](img/github-mark.svg) [github.com/pyodide/pyodide](https://github.com/pyodide/pyodide)

  * python distribution compiled to WebAssembly
  * runs in the browser
  * includes numpy, pandas, matplotlib, etc...
  *  **write wasm kernels**

</div>
<div>

R-Lang:
![width:34px](img/github-mark.svg)[github.com/r-wasm/webr](https://github.com/r-wasm/webr):
 * R interpreter compiled to WebAssembly
 * runs in the browser
 * includes packages compiled to WebAssembly
*  **write wasm kernels**

</div>


</div>

---
<style>section { justify-content: start; }</style>

![bg contain](img/jlite.svg)


---
![height:120px](img/jlite.svg)

  * ![h:30px](img/github-mark.svg) [github.com/jupyterlite/jupyterlite](https://github.com/jupyterlite/jupyterlite)
  * JupyterLab distribution that runs entirely in the browser 
  * Wasm powered kernels running in the browser

  * **JupyterCon**: Creating interactive Jupyter websites with JupyterLite: 
  ![h:30px](img/github-mark.svg)  https://github.com/jtpio/jupytercon-2023-jupyterlite


---

<iframe
src="https://jupyterlite.github.io/demo/lab/index.html"
width="100%"
height="500px"
>
</iframe>


--- 

<style>section { justify-content: start; }</style>

# XeusLite: Xeus kernels for JupyterLite

![h:500px center](img/xeuslite.webp)

---

# Architecture of xeus

![bg fit right](img/xeus_archi_previous.svg)

* ![h:30px](img/github-mark.svg) [github.com/jupyter-xeus/xeus](https://github.com/jupyter-xeus/xeus)
* Customizable via
    
    * Custom Interpreter
    * Custom Debugger
    * Custom Server
  
* Hard coded to use ZeroMQ
  
    * ZeroMQ is not availalbe when compiling for Wasm


---

# Architecture of xeus (now)

![bg fit right](img/xeus_archi.svg)
<style scoped>
li {
   font-size: 0.89rem;
}
</style>



* Make xeus agnostic to the communication layer
* Extract `zmq` based server in dedicated package:
  ![h:30px](img/github-mark.svg) [github.com/jupyter-xeus/xeus-zmq](https://github.com/jupyter-xeus/xeus-zmq)

* Implement Server with `wasm` compatible communication layer:
  ![h:30px](img/github-mark.svg) [github.com/jupyter-xeus/xeus-lite](github.com/jupyter-xeus/xeus-lite)

---

# Usage of Xeus Kernels with JupyterLite

![h:500px center](img/wasm_piecewise/wasm7.svg)

---

# Usage of Xeus Kernels with JupyterLite

![h:500px center](img/wasm_piecewise/wasm6.svg)

---

# Usage of Xeus Kernels with JupyterLite

![h:500px center](img/wasm_piecewise/wasm5.svg)

---

# Usage of Xeus Kernels with JupyterLite

![h:500px center](img/wasm_piecewise/wasm4.svg)

---

# Usage of Xeus Kernels with JupyterLite

![h:500px center](img/wasm_piecewise/wasm3.svg)

---

# Usage of Xeus Kernels with JupyterLite

![h:500px center](img/wasm_piecewise/wasm2.svg)

---

# Usage of Xeus Kernels with JupyterLite

![h:500px center](img/wasm_piecewise/wasm1.svg)

---

# Usage of Xeus Kernels with JupyterLite

![h:500px center](img/wasm_piecewise/wasm0.svg)



--- 
# Examples of Xeus-Lite Kernels


<div class="grid grid-cols-2 grid-rows-auto gap-4">

<div>

![width:200px](img/xeus-python-logo.svg) ![width:200px](img/python_gif.gif)

</div>
<div>

![width:200px](img/xeus-lua-logo.svg)  ![width:200px](img/lua.gif)

</div>



<div>

![width:200px](img/xeus-sqlite-logo.svg) ![width:200px](img/xeus-sqlite-screenshot.png)

</div>

<div>

![width:200px](img/xeus-wren-logo.svg) ![width:200px](img/wren_gif.gif)

</div>
<div>

![width:200px](img/xeus-nelson-logo.svg)

</div>

</div>

----

# Applications

## Embed REPL
```html
<iframe
  src="https://jupyterlite.github.io/demo/repl/index.html?kernel=Lua&toolbar=1"
  width="100%"
  height="500px"
>
</iframe>
```

----
## Embed REPL

<iframe
  src="https://jupyterlite.github.io/demo/repl/index.html?kernel=Lua&toolbar=1"
  width="100%"
  height="500px"
>
</iframe>

----

## Embed JupyterLite

```html
<iframe
src="https://jupyterlite.github.io/demo/lab/index.html"
width="100%"
height="500px"
>
</iframe>
```
---
## Embed JupyterLite 

<iframe
src="https://jupyterlite.github.io/demo/lab/index.html"
width="100%"
height="500px"
>
</iframe>

---

# Deploying Xeus Python
-  https://github.com/jupyterlite/xeus-python-demo

  ![height:350px center](img/deploy.gif)

----

# Outlook
  * improve xeus-lite kernels:
      * dynamic loading of conda packages with mamba
      * dynamic loading of pip packages with pip
  * implement more xeus-lite kernels:
      * xeus-cpp
      * xeus-r 
  * improve testing for xeus-lite kernels
  * ability to generate lite kernels repos from regular kernel repos
  
----

Resources

- Jupyter documentation: https://docs.jupyter.org
- xeus documentation: https://xeus.readthedocs.io
- This presentation: https://derthorsten.github.io/xeus-kernels-browser

----

![bg content](img/katze-kostuem.jpg)
