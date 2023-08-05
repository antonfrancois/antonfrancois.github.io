---
layout: page
title: my PhD in short. 
description: a short summary of my PhD project (in construction).
img: assets/img/vol_rend_reg.gif
importance: 1
category: academic
---

<style>
#my-iframe {
  display: block;
  margin: 0 auto;
}
</style>



One can find the full document here : <a href="https://www.theses.fr/s228301">theses.fr</a> or directly here : <a href = "https://helios2.mi.parisdescartes.fr/~afrancoi/AntonFRANCOIS_files/Manuscrit_Anton.pdf">PhD Dissertation</a>

In this page I start by giving the actual abstract of my thesis. Then I will do a short and simplified explanation of the different contribution of my PhD. 

Note : Si vous voulez lire en Français, des versions du résumé et du chapitre 1 traduites sont disponibles dans le manuscrit de thèse. Le chapitre 1 couvre les notions de bases nécessaires à comprendre mon projet de thèse sans rentrer trop dans les détails techniques.

## My Thesis's Abstract


This thesis addresses the problem of registering images with different topologies with diffeomorphic deformation. We focus on the case of medical images of glioblastomas, a type of brain tumour.

Firstly, we implemented both Metamorphosis and LDDMM for images in 2D and 3D. Our implementation is object-oriented and developed using PyTorch, allowing for versatility in usage and easy modifications. We also used a semi-Lagrangian scheme on both images and residual.The implementation is GPU-accelerated, and we demonstrate the effectiveness of our approach through experiments on glioblastomas using BraTS datasets.

Secondly, we address the difficulties associated with the Metamorphosis algorithm by proposing a framework for incorporating prior knowledge into the model, called Constrained Metamorphosis. The framework allows for adding constraints on the registration problem by also matching given priors. We present two specific types of priors that can be incorporated into the model; a growing mask generated from a given segmentation and a field that guides the deformation in a desired direction. We demonstrate the effectiveness of our approach through experiments on glioblastomas using BraTS datasets, comparing with state-of-the- art methods.

Finally, we developed a tumour segmentation tool using Topological Data Analysis (TDA) to detect characteristic components within the FLAIR and T1ce modalities.



## Comic books 

<p style='text-align: justify; '>
In addition to the traditional academic writing, my PhD thesis also includes two comics that explain some of the key concepts in my research in a way that is accessible to non-scholars. The comics are designed to be engaging and informative, and they use humor and imagery to help explain complex ideas.
</p>
   
<p style='text-align: justify; '>
The beautiful artworks were made by Salomé Govignon, and she and I are the main characters of the comics. In the comics, she plays the role of the candid student and I guide her through different concepts.
</p>
   
<p style='text-align: justify; '>
The first comic explains the concept of "diffeomorphic shape spaces," which is a key concept in my research. I decided to explain it from the image perspective, as this is the type of data I use. The second comic explains the concept of "semi-Lagrangian schemes," which is one important concept for implementing image transport.
</p>
   
<p style='text-align: justify; '>
I believe that the comics in my thesis will help to make my research more accessible to a wider audience. They are a fun and engaging way to learn about some of the key concepts in my research, and they can help to demystify some of the more complex ideas.
</p>
   

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bd_0.png" title="comic preview" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bd_1.png" title="comic preview" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bd_2.png" title="comic preview" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Two versions available to Download:
    <ul style="list-style-type: none;">
        <li><a href="https://helios2.mi.parisdescartes.fr/~afrancoi/AntonFRANCOIS_files/BD_env2.pdf">-- Comic in english --</a></li>
        <li><a href="https://helios2.mi.parisdescartes.fr/~afrancoi/AntonFRANCOIS_files/BD_frv2.pdf">-- BD en français --</a></li>
    </ul>
</div>


# The first open-source implementation of Metamorphoses.

## Some theoritical background

The Metamorphic framework lies on [Large Deformation Diffeomorphic Metric Mapping (LDDMM)](https://en.wikipedia.org/wiki/Large_deformation_diffeomorphic_metric_mapping). In short it is a registration technic that use flows of vectors fields to match two objects, in our cases images. The flow of vectors field is the solution of the ordinary differential equation:
$$\dot \varphi_t = v_t \circ \varphi_t$$   
where $(v_t)_{t\in [0,1]}$ is a temporal vector field belonging to an admissible vector space $V$, $\varphi_t$ is the deformation solution of this equation and $\dot \varphi$ the derivation relative to time. Then the deformation $J$ of an image $I$ by the deformation $\varphi$ is given by the relation:
$$J = I \circ \varphi^{-1}.$$
LDDMM is a widely studied method and the state of the art for precise registrations. However, because of the Diffeomorphic assumption, it can be used only to match images of the same topology. For example, two images of 'healthy' faces have the same topology, because both have two eyes, one mouth, etc.. However, a cyclops, having one eye only have a different topology. 


<div class="row" id="my-iframe">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/phd/faces.png" title="faces to demonstrate topology differences" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    faces to demonstrate topology differences
</div>

   
Metamorphosis is a method that register two images with a diffeomorphism but also allows to add intensity differences to given pixels. In fact, one can write the image evolution like so:
$$\dot I_t = I_t\circ \varphi_t + z_t$$
Here, $z_t$ is something similar to an image, the only difference being that it can have negative values. Hence, in theory, any pair of image could be matched.


## Some implementation details

   
I will not get into the details here, and please follow the Chapter 2 of my thesis if you want to have a complete explanation with references. The theory translate the registration problem as finding a path in an abstract space and is looking for the shortest path among all that perform the perfect match. We know that the shortest path is among the geodesics, a generalization of the straight line. Theorems gives us the formulation for those geodesics in the form of a PDE system that indicate how to transport our images. However, in practice it is hard to find a path that perform a matching. It is why algorithmically we take our image $I_0$ a direction at random (i.e.: $v_0$), follow the PDE system and take the transported image $I_1$. At this stage, we are able to compare $I_1$ and the target image. Then we modify the initial direction until we get our transported image close enough to the target one. This processed is called _geodesic shooting_ and it is summarized in the slide bellow.


<iframe src="https://slides.com/antonfrancois/deck-d1ea90/embed#/3/3" width="576" height="420" title="Anton François - PhD Defense" id="my-iframe" class="my-class" data-slide="3" data-presentation="deck-d1ea90"></iframe>
<div class="caption">
    Slides from my PhD defense.
</div>

As mentioned in the previous paragraph, to obtain image $I_1$​, one needs to integrate a partial differential equation (PDE) system. I chose to use semi-Lagrangian schemes for this task. I will not go into the technical details here, as they are well-explained in Section 2.5 of my manuscript. However, you can think of semi-Lagrangian schemes as a compromise between Eulerian and Lagrangian schemes, two classical ways to integrate PDE systems. One novelty of my implementation is that I used semi-Lagrangian schemes in a way that significantly decreased the number of computations required, while still maintaining accuracy.

<div class="row">
    <div class="col col-lg-2">
        {% include figure.html path="assets/img/phd/fluids.gif" title="comic preview" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-md-auto">
        {% include figure.html path="assets/img/phd/semi-Lagrangian_scheme.png" title="comic preview" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: An image integration example that demonstrates how close our model behave to a non-difusive fluid. Right: Illustration of the semi-Lagrangian scheme.
</div>

<!-- _________________________________

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
{% endraw %} -->
