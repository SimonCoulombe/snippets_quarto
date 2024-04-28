---
title: Quelles villes perdent leur français?
author: Simon
date: '2022-08-19'
slug: []
categories:
  - Rstats
tags:
  - cancensus
  - francais
keywords:
  - tech
---



<script src="/rmarkdown-libs/htmlwidgets/htmlwidgets.js"></script>
<script src="/rmarkdown-libs/pymjs/pym.v1.js"></script>
<script src="/rmarkdown-libs/widgetframe-binding/widgetframe.js"></script>


<p>Les données de langue du Recensement de 2021 sont sorties cette semaine et elles ont déjà été ajoutées à l’excellent package {cancensus} de Jens von Bergmann. (merci!)</p>
<p>Je me demandais quelles villes du Québec perdent le plus leur français. Ma définition (c’est mon blog, c’est moi qui décide) de perdre le français, c’est que le pourcentage de gens dont la première langue officielle parlée est le français diminue entre 2016 et 2021.</p>
<p>On va utiliser les packages {cancensus} pour le data du recensement, {dplyr} pour le data wrangling, {sf} pour le spatial data wrangling et {mapview} pour créer une carte leaflet sans trop se casser le bécyke.</p>
<p>Faut commencer par trouver les variables de langue..</p>
<p>On utilise la fonction list_census_vectors() pour trouver toutes les variables variables du recensement de 2021 contenant le mot “language”. Il y en a plus de 1000. On est chanceux, le vecteur qu’on veut (personnes dont la première langue officieille parlée est le français ) est la 8e dans la liste : “Language; First official language spoken for the total population excluding institutional residents; French”. Il s’agit du vecteur “v_CA21_1165”.</p>
<div id="htmlwidget-1" style="width:100%;height:1000px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"url":"/oldposts/2022-08-19-quelles-villes-perdent-leur-fran-ais/index.en-us_files/figure-html/widgets/widget_unnamed-chunk-1.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script>
<p>On va devoir trouver le “parent” du vecteur pour avoir la population totale qui a répondu à la question. C’est la fonction parent_census_vector(), et elle va nous dire qu’il s’agit du vecteur “v_CA21_1159”</p>
<pre><code>## # A tibble: 1 × 7
##   vector      type  label                units parent_vector aggregation details
##   &lt;chr&gt;       &lt;fct&gt; &lt;chr&gt;                &lt;fct&gt; &lt;chr&gt;         &lt;chr&gt;       &lt;chr&gt;  
## 1 v_CA21_1159 Total First official lang… Numb… &lt;NA&gt;          Additive    CA 202…</code></pre>
<p>On fait la même chose pour 2016, on va trouver les vecteurs v_CA16_533(français) et v_CA16_527 (total)</p>
<div id="htmlwidget-2" style="width:100%;height:1000px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"url":"/oldposts/2022-08-19-quelles-villes-perdent-leur-fran-ais/index.en-us_files/figure-html/widgets/widget_unnamed-chunk-3.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script>
<pre><code>## # A tibble: 1 × 7
##   vector     type  label                 units parent_vector aggregation details
##   &lt;chr&gt;      &lt;fct&gt; &lt;chr&gt;                 &lt;fct&gt; &lt;chr&gt;         &lt;chr&gt;       &lt;chr&gt;  
## 1 v_CA16_527 Total Total - First offici… Numb… &lt;NA&gt;          Additive    CA 201…</code></pre>
<p>On va télécharger les données de langue au niveau de la ville (CSD) pour les deux recensements avec la fonction get_census(). On crée ensuite les variable pct_not_french2016 et pct_not_french2021 qui représente le pourcentage de personnes qui n’ont pas le français comme première langue officielle dans la ville.</p>
<p>Ensuite, on join les 2 bases de données selon la geo_uid (le numéro de ville) et on calcule “diff”, soit pct_not_french2021 moins pct_not_french2016. En dessous on va montrer un beau graphique et une carte de diff_max10, soit la différence cappée à 10% pour faire une belle carte.</p>
<p>Les pires municipalités..
(bon y’a un -10% qu’il faudrait investiguer à Saint-Guy)</p>
<div id="htmlwidget-3" style="width:100%;height:1000px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-3">{"x":{"url":"/oldposts/2022-08-19-quelles-villes-perdent-leur-fran-ais/index.en-us_files/figure-html/widgets/widget_unnamed-chunk-6.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script>
<p>La carte</p>
<div id="htmlwidget-4" style="width:100%;height:500px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-4">{"x":{"url":"/oldposts/2022-08-19-quelles-villes-perdent-leur-fran-ais/index.en-us_files/figure-html/widgets/widget_unnamed-chunk-7.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script>