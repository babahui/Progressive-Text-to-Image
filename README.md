![Python >=3.5](https://img.shields.io/badge/Python->=3.5-yellow.svg)
![PyTorch >=1.0](https://img.shields.io/badge/PyTorch->=1.6-blue.svg)

# Progressive Text-to-Image Diffusion with Soft Latent Direction

The *official* repository for Progressive Text-to-Image Diffusion with Soft Latent Direction.

## News
- 2023.09  Code will be released coming soon.

## Progressive Text-to-Image

![framework](figs/teaser-8-13.pdf)

Existing text-to-image synthesis approaches struggle with textual prompts involving multiple entities and specified relational directions. We propose to decompose the protracted prompt into a set of short commands, including synthesis, editing and erasing operations, using a Large Language Model (LLM) and progressively generate the image. Our strategy enhances both controllability and fidelity and allows for interactive modifications from user interference at each generation step.

## Pipeline

![framework](figs/pipeline-8-15.pdf)

Overview of our unified framework emphasizes progressive synthesis, editing, and erasing. In each progressive step, A random latent \(z_t\) is directed through the cross-attention map in inverse diffusion. Specifically, we design a soft stimulus loss that evaluates the positional difference between entity attention and the target mask region, leading to a gradient for updating the latent \(z_{t-1}^{*}\) as a latent response. Subsequentially, another forward diffusion pass is applied to denoise \(z^*_{t}\), yielding deriving \(z^{*}_{t-1}\). In the latent fusion phase, we transform the previous \(i\)-th image into a latent code \(z^{bg}_{t-1}\) using DDIM inversion. The blending of \(z^{*}_{t-1}\) with \(z^{bg}_{t-1}\) incorporates a dynamic evolving mask, which starts with a layout box and gradually shifts to cross-attention. Finally, \(z^{*}_{t-1}\) undergoes multiple diffusion reverse steps and results in the \((i+1)\)-th image.
