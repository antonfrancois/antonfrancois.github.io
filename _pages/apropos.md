---
layout: about
title: à propos
permalink: /
# subtitle:  in short

profile:
  align: right
  image: anton_pic.png
  image_circular: true # crops the image to make it circular
  address: #>
#  <p>anton *dot* francois134 'at' gmail *dot* com </p>

news: false  # includes a list of news items
latest_posts: false  # includes a list of the newest posts
selected_papers: true # includes a list of papers marked as "selected={true}"
social: true  # includes social icons at the bottom of the page
importance: 1
---

**Je suis actuellement en post-doctorat à l’ENS Paris-Saclay, au sein du Centre Borelli. Je participe au projet ANR RADIOAIDE, qui vise à mieux comprendre la leucoencéphalopathie de la substance blanche — une pathologie dégénérative survenant chez certains patients traités par radiothérapie pour des cancers cérébraux.**
Dans ce cadre, je suis en charge du développement de méthodes de recalage d’images, dont l’objectif est d’établir des correspondances morphologiques et géométriques entre différentes IRM acquises longitudinalement chez les patients.  
L’objectif final du projet est de reconstruire des trajectoires spatio-temporelles des voxels cérébraux et d’estimer des marqueurs géométriques (croissance, atrophie, déformation locale) permettant de caractériser les signatures évolutives de la leucoencéphalopathie post-thérapeutique.


**Depuis ma thèse, je développe et maintiens la librairie _Demeter-Metamorphosis_, qui implémente l’algorithme des Métamorphoses — une extension du cadre LDDMM (_Large Deformation Diffeomorphic Metric Mapping_) — conçue pour le recalage d’images dans des contextes où la topologie peut varier entre les images source et cible.**  
Ces méthodes s’inscrivent dans le cadre théorique de l’**espace des formes**, dont l’objectif est de modéliser, quantifier et représenter les variations géométriques au sein d’une population de formes, en tenant compte à la fois des déformations diffeomorphes et des variations d’intensité ou de structure.

Mon sujet de recherche est à l'interface de plusieurs grand domaine des mathématiques appliquées : 
- La **Géométrie Différentielle** qui constitue le socle théorique de l’espace des formes et permet de modéliser les déformations via des structures riemanniennes.
- L'**Optimisation** utilisée pour résoudre les problèmes de recalage sous contraintes variées (régularisation, attache aux données, conservation de structures).
- L'**Analyse d'image** (et plus généralement du signal) qui regroupe un large ensemble de techniques dédiées au traitement, à la transformation et à l’extraction d’informations à partir de données pixelisées.
- L'**Analyse numérique des EDP**, car dans les Métamorphoses la dynamique des images est décrite à l’aide de modèles inspirés de la mécanique des fluides
- L'**Informatique**: En effet je code et doit comprendre la gestion des ressources de calculs comme la puissance de calcul et la mémoire (RAM et GPU).

