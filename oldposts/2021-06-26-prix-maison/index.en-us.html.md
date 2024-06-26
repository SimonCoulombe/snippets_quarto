---
title: Où sont les maisons abordables?
author: Simon
date: '2021-06-26'
slug: prix_maison
categories: []
tags: []
keywords:
  - tech
thumbnailImage: "/oldposts/2021-06-26-prix-maison/index.en-us_files/1624883913993.jpeg" 
thumbnailImagePosition: left    
---



<script src="/rmarkdown-libs/header-attrs/header-attrs.js"></script>


<p>Here I combine two data sources to find the cities with the most affordable houses.<br />
We use the median house price fro m2018 as provided by “JLR solutions immobilières” and the median total household income for families with 2 adults for 2018 provided by Statistics Canada.</p>
<p><img src="/oldposts/2021-06-26-prix-maison/index.en-us_files/figure-html/unnamed-chunk-3-1.png" width="1344" style="display: block; margin: auto;" /></p>
<p><img src="/oldposts/2021-06-26-prix-maison/index.en-us_files/figure-html/unnamed-chunk-4-1.png" width="1344" style="display: block; margin: auto;" /></p>
<p><img src="/oldposts/2021-06-26-prix-maison/index.en-us_files/figure-html/unnamed-chunk-5-1.png" width="1344" style="display: block; margin: auto;" /></p>
<pre><code>## # A tibble: 168 x 7
##    geo                geo_uid  value RMRNOM     RMRPIDU PRIDU PRNOM             
##    &lt;chr&gt;              &lt;chr&gt;    &lt;dbl&gt; &lt;chr&gt;      &lt;chr&gt;   &lt;chr&gt; &lt;chr&gt;             
##  1 St. John&#39;s, Newfo… 001     113050 St. John&#39;s 10001   10    Newfoundland and …
##  2 Bay Roberts, Newf… 005      85010 Bay Rober… 10005   10    Newfoundland and …
##  3 Grand Falls-Winds… 010      82630 Grand Fal… 10010   10    Newfoundland and …
##  4 Gander, Newfoundl… 011      98590 Gander     10011   10    Newfoundland and …
##  5 Corner Brook, New… 015      89760 Corner Br… 10015   10    Newfoundland and …
##  6 Non CMA-CA, Newfo… 10000    77540 &lt;NA&gt;       &lt;NA&gt;    &lt;NA&gt;  &lt;NA&gt;              
##  7 Charlottetown, Pr… 105      91430 Charlotte… 11105   11    Prince Edward Isl…
##  8 Summerside, Princ… 110      80560 Summerside 11110   11    Prince Edward Isl…
##  9 Non CMA-CA, Princ… 11100    83910 &lt;NA&gt;       &lt;NA&gt;    &lt;NA&gt;  &lt;NA&gt;              
## 10 Halifax, Nova Sco… 205     101550 Halifax    12205   12    Nova Scotia / Nou…
## # … with 158 more rows</code></pre>
<p><img src="/oldposts/2021-06-26-prix-maison/index.en-us_files/figure-html/unnamed-chunk-6-1.png" width="1344" style="display: block; margin: auto;" />
<img src="/oldposts/2021-06-26-prix-maison/index.en-us_files/figure-html/unnamed-chunk-7-1.png" width="1344" style="display: block; margin: auto;" /></p>
<p><img src="/oldposts/2021-06-26-prix-maison/index.en-us_files/figure-html/unnamed-chunk-8-1.png" width="1344" style="display: block; margin: auto;" /></p>
<p><img src="animated_gif2.gif" /></p>
