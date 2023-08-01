---
layout: page
title: Registering Glioblastoma
description: a project with a background image
img: assets/img/12.jpg
importance: 1
category: work
---

One can find the full document here : <a href="https://www.theses.fr/s228301">theses.fr</a>

# My Thesis's Abstract
This thesis addresses the problem of registering images with different topologies with diffeomorphic deformation. We focus on the case of medical images of glioblastomas, a type of brain tumour.

 Firstly, we implemented both Metamorphosis and LDDMM for images in 2D and 3D. Our implementation is object-oriented and developed using PyTorch, allowing for versatility in usage and easy modifications. We also used a semi-Lagrangian scheme on both images and residual.The implementation is GPU-accelerated, and we demonstrate the effectiveness of our approach through experiments on glioblastomas using BraTS datasets.
 
 Secondly, we address the difficulties associated with the Metamorphosis algorithm by proposing a framework for incorporating prior knowledge into the model, called Constrained Metamorphosis. The framework allows for adding constraints on the registration problem by also matching given priors. We present two specific types of priors that can be incorporated into the model; a growing mask generated from a given segmentation and a field that guides the deformation in a desired direction. We demonstrate the effectiveness of our approach through experiments on glioblastomas using BraTS datasets, comparing with state-of-the- art methods.
 
 Finally, we developed a tumour segmentation tool using Topological Data Analysis (TDA) to detect characteristic components within the FLAIR and T1ce modalities.


- Faire une visualisation de mes BDs
- trouver des images, figures sexy (ex: gif dynamiques des fluides.)
- mettre la vidéo de ma soutenance de thèse.
- mettre le lien vers mes slides.
- faire un résumé des contributions, vulgarisés
_________________________________

Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
