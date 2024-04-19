---
title: Combien rapporterait la taxe sur la richesse de QS ?
description: "On vérifie avec le PUMF"
author: Simon Coulombe
date: '2022-09-08'
slug: combien-taxe-richesse
categories:
  - rstats
  - pumf
  - ESF
  - qc2022
  - ultra-riches
lang: fr  
---





Ça parle beaucoup d'impôt sur le patimoine (ou avoir net) ces temps-ci au Québec!

Dans un post précédent, j'ai validé la proportion des gens qui seraient touchés par la taxe sur la richesse proposée.

[Rappelons les paramètres](https://www.lesoleil.com/2022/09/06/les-grands-fortunes-dans-la-mire-fiscale-de-quebec-solidaire-4fe7386f5fb8cbea5defbaa3684795e8):

Impôt sur les grandes fortunes :

* Le premier million d'actifs net est exempté d’impôt  
* Entre 1 million et 9,9 millions: 0,1% de l’actif net
* Entre 10 millions et 99 millions: 1% de l’actif net
* Plus de 100 millions: 1,5% de l’actif net

La question que je me pose aujourd'hui:
- Combien est-ce qu'on peut aller chercher avec cette taxe là?  
- Combien est-ce qu'on perdrait en fichant la paix aux gens en bas de 2 millions?  3?

let's gooo


# Les données   

On a découvert hier une super source de données:  le PUMF de l'Enquête sur la Sécurité Financière du Statistiques Canada.  
[On en a parlé hier](https://www.simoncoulombe.com/2022/09/ultra-riches/) et [plus tôt aujourd'hui](https://www.simoncoulombe.com/2022/09/impot-foncier/), c'était super intéressant, allez voir 

Il comporte 2003 les données de 2003 ménages au Québec, chacun ayant un poids échantillonal entre 150 et 8000.

Les variables que l'on va utiliser sont les suivantes:  


PWNETWT : valeur nette de l'unité familliale (base de terminaison).  
PFMTYPG : le type de famille 


Voici les types de familles possibles :


::: {.cell}
::: {.cell-output .cell-output-stdout}

```
# A tibble: 5 × 2
  PFMTYPG type_menage                                      
  <chr>   <chr>                                            
1 1       Personne seule                                   
2 2       Couple, sans enfant                              
3 3       Couple, avec des enfants et famille monoparentale
4 4       Autres types de famille                          
5 9       Non déclaré                                      
```


:::
:::


Le problème c'est que la taxe de QS serait sur l'avoir net de l'individu et que nous disposons de l'avoir net du ménage.
On va faire l'hypothèse (assez forte), que les adultes dans le ménage vont se partager à part égales l'avoir net afin de minimiser leur charge fiscale.

Un problème important subsite:  pour les types de familles #3, #4 et #5 il pourrait y avoir 1 ou 2 adultes.

Nous allons donc faire deux scénarios: Le "impôt maximum", où l'on suppose qu'il n'y a qu'un seul adulte et le scénario "impôt minimum" où l'o suppose qu'il y a deux adultes.  

# Les manips   

::: {.cell}

:::

::: {.cell}

:::


* Le premier million d'actifs net est exempté d’impôt  
* Entre 1 million et 9,9 millions: 0,1% de l’actif net
* Entre 10 millions et 99 millions: 1% de l’actif net
* Plus de 100 millions: 1,5% de l’actif net




Voici à quoi ressemblent les micro-données brutes préparées (et triées en ordre descendant d'avoir net)

::: {.cell}
::: {.cell-output .cell-output-stdout}

```
# A tibble: 2,003 × 16
   PWNETWPT PWEIGHT PWAPRVAL PWASTRST PAGEMIEG PFMTYPG gr_age  type_menage
      <dbl>   <dbl>    <dbl>    <dbl> <chr>    <chr>   <chr>   <chr>      
 1 17741925   1187.   950000  1650000 08       9       45-54   Non déclaré
 2 16090000    569.        0        0 12       9       65-plus Non déclaré
 3 14336450   1775.   420000  2500000 10       9       55-64   Non déclaré
 4 13824500   1105.  1000000   875000 08       9       45-54   Non déclaré
 5 11528400   1581.   280000        0 10       9       55-64   Non déclaré
 6 10427000    781.   775000    75000 08       9       45-54   Non déclaré
 7 10425000    837.   525000   475000 10       9       55-64   Non déclaré
 8  9625000    557.   925000        0 12       9       65-plus Non déclaré
 9  9582500    661.  1400000  4900000 09       9       55-64   Non déclaré
10  8812500   2033.   725000        0 06       9       35-44   Non déclaré
# ℹ 1,993 more rows
# ℹ 8 more variables: nombre_adulte_scenario_min <dbl>,
#   nombre_adulte_scenario_max <dbl>, valeur_par_adulte_scenario_min <dbl>,
#   valeur_par_adulte_scenario_max <dbl>, taxe_par_adulte_scenario_min <dbl>,
#   taxe_par_adulte_scenario_max <dbl>, taxe_totale_scenario_min <dbl>,
#   taxe_totale_scenario_max <dbl>
```


:::
:::



Vous pouvez voir que le ménage le plus cher de l'échantillon a une valeur nette de 17 741 925$ (PWNETWPT) et qu'il représente 1186 ménages (PWEIGHT). 
Apparemment on n'est pas tombés sur les Desmarais.

Première déception:  leur type de ménage (PFMTYPG) est le "9", soit "Non déclaré".  
Deuxième déception:  c'est le cas de 31 des 33 ménages les plus riches de l'échantillon.  C'est probablement pour mieux préserver la confidentialité de nos riches.  


Ça fait une sacré différence selon le scénario.  Pour le ménage le plus riche, un seul individu valant 17M paierait 86 419\$, tandis que deux individus valant 8.8M paieraient seulement 7 870\$ pour un total de 15 741 \$.   

On récupèrerait  donc plus de 5x plus d'argent dans le premier scénario.


Voici quand même la valeur totale qu'on obtient au Québec dans les 2 scénarios, ainsi que dans un scénario où la moitié des familles dont on ne connait pas la taille sont composées d'une personne 
seul et l'autre moitié d'un couple.



::: {.cell}
::: {.cell-output-display}


```{=html}
<div id="ceklnsdomm" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:1080px;height:auto;">
<style>#ceklnsdomm table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#ceklnsdomm thead, #ceklnsdomm tbody, #ceklnsdomm tfoot, #ceklnsdomm tr, #ceklnsdomm td, #ceklnsdomm th {
  border-style: none;
}

#ceklnsdomm p {
  margin: 0;
  padding: 0;
}

#ceklnsdomm .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#ceklnsdomm .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#ceklnsdomm .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#ceklnsdomm .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#ceklnsdomm .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#ceklnsdomm .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ceklnsdomm .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#ceklnsdomm .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#ceklnsdomm .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#ceklnsdomm .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#ceklnsdomm .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#ceklnsdomm .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#ceklnsdomm .gt_spanner_row {
  border-bottom-style: hidden;
}

#ceklnsdomm .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#ceklnsdomm .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#ceklnsdomm .gt_from_md > :first-child {
  margin-top: 0;
}

#ceklnsdomm .gt_from_md > :last-child {
  margin-bottom: 0;
}

#ceklnsdomm .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#ceklnsdomm .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#ceklnsdomm .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#ceklnsdomm .gt_row_group_first td {
  border-top-width: 2px;
}

#ceklnsdomm .gt_row_group_first th {
  border-top-width: 2px;
}

#ceklnsdomm .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#ceklnsdomm .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#ceklnsdomm .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#ceklnsdomm .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ceklnsdomm .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#ceklnsdomm .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#ceklnsdomm .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#ceklnsdomm .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#ceklnsdomm .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ceklnsdomm .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#ceklnsdomm .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#ceklnsdomm .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#ceklnsdomm .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#ceklnsdomm .gt_left {
  text-align: left;
}

#ceklnsdomm .gt_center {
  text-align: center;
}

#ceklnsdomm .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#ceklnsdomm .gt_font_normal {
  font-weight: normal;
}

#ceklnsdomm .gt_font_bold {
  font-weight: bold;
}

#ceklnsdomm .gt_font_italic {
  font-style: italic;
}

#ceklnsdomm .gt_super {
  font-size: 65%;
}

#ceklnsdomm .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#ceklnsdomm .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#ceklnsdomm .gt_indent_1 {
  text-indent: 5px;
}

#ceklnsdomm .gt_indent_2 {
  text-indent: 10px;
}

#ceklnsdomm .gt_indent_3 {
  text-indent: 15px;
}

#ceklnsdomm .gt_indent_4 {
  text-indent: 20px;
}

#ceklnsdomm .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <caption>Données PUMF ESF Statcan pour le Québec 2019, calculs @coulsim</caption>
  <thead>
    <tr class="gt_heading">
      <td colspan="9" class="gt_heading gt_title gt_font_normal gt_bottom_border" style>Taxe sur la richesse récoltée selon le type de ménage</td>
    </tr>
    
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre d'observations">Nombre d'observations</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre pondéré de ménages">Nombre pondéré de ménages</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario minimal">Nombre de ménages taxés dans le scénario minimal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario maximal">Nombre de ménages taxés dans le scénario maximal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario minimal">Taxe totale perçue dans le scénario minimal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario maximal">Taxe totale perçue dans le scénario maximal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario 50-50">Nombre de ménages taxés dans le scénario 50-50</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario 50-50">Taxe totale perçue dans le scénario 50-50</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub">Non déclaré</th>
<td headers="stub_1_1 nombre_observations" class="gt_row gt_right">63</td>
<td headers="stub_1_1 nombre_observations_ponderees" class="gt_row gt_right">66,791</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_min" class="gt_row gt_right">34,918</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_max" class="gt_row gt_right">50,891</td>
<td headers="stub_1_1 taxe_totale_scenario_min" class="gt_row gt_right">218,486,324</td>
<td headers="stub_1_1 taxe_totale_scenario_max" class="gt_row gt_right">508,240,648</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">42,904</td>
<td headers="stub_1_1 taxe_totale_scenario_50_50" class="gt_row gt_right">363,363,486</td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub">Autres types de famille</th>
<td headers="stub_1_2 nombre_observations" class="gt_row gt_right">233</td>
<td headers="stub_1_2 nombre_observations_ponderees" class="gt_row gt_right">486,400</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_min" class="gt_row gt_right">33,906</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_max" class="gt_row gt_right">130,884</td>
<td headers="stub_1_2 taxe_totale_scenario_min" class="gt_row gt_right">29,165,117</td>
<td headers="stub_1_2 taxe_totale_scenario_max" class="gt_row gt_right">94,274,574</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">82,395</td>
<td headers="stub_1_2 taxe_totale_scenario_50_50" class="gt_row gt_right">61,719,846</td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub">Couple, avec des enfants et famille monoparentale</th>
<td headers="stub_1_3 nombre_observations" class="gt_row gt_right">442</td>
<td headers="stub_1_3 nombre_observations_ponderees" class="gt_row gt_right">759,009</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_min" class="gt_row gt_right">21,727</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_max" class="gt_row gt_right">92,254</td>
<td headers="stub_1_3 taxe_totale_scenario_min" class="gt_row gt_right">14,986,027</td>
<td headers="stub_1_3 taxe_totale_scenario_max" class="gt_row gt_right">61,369,005</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">56,990</td>
<td headers="stub_1_3 taxe_totale_scenario_50_50" class="gt_row gt_right">38,177,516</td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub">Couple, sans enfant</th>
<td headers="stub_1_4 nombre_observations" class="gt_row gt_right">626</td>
<td headers="stub_1_4 nombre_observations_ponderees" class="gt_row gt_right">969,261</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_min" class="gt_row gt_right">66,396</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_max" class="gt_row gt_right">66,396</td>
<td headers="stub_1_4 taxe_totale_scenario_min" class="gt_row gt_right">61,172,283</td>
<td headers="stub_1_4 taxe_totale_scenario_max" class="gt_row gt_right">61,172,283</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">66,396</td>
<td headers="stub_1_4 taxe_totale_scenario_50_50" class="gt_row gt_right">61,172,283</td></tr>
    <tr><th id="stub_1_5" scope="row" class="gt_row gt_left gt_stub">Personne seule</th>
<td headers="stub_1_5 nombre_observations" class="gt_row gt_right">639</td>
<td headers="stub_1_5 nombre_observations_ponderees" class="gt_row gt_right">1,567,880</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_min" class="gt_row gt_right">82,177</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_max" class="gt_row gt_right">82,177</td>
<td headers="stub_1_5 taxe_totale_scenario_min" class="gt_row gt_right">59,757,455</td>
<td headers="stub_1_5 taxe_totale_scenario_max" class="gt_row gt_right">59,757,455</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">82,177</td>
<td headers="stub_1_5 taxe_totale_scenario_50_50" class="gt_row gt_right">59,757,455</td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">sum</th>
<td headers="grand_summary_stub_1 nombre_observations" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">2003</td>
<td headers="grand_summary_stub_1 nombre_observations_ponderees" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">3849341</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_min" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">239123.8</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_max" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">422603.4</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_min" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">383567206</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_max" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">784813965</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">330863.6</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_50_50" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">584190586</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::



En 2019, la taxe de Québec solidaire aurait permis de récolter entre 383M et 784M dans les 2 scénarios extrêmes, avec un chiffre de scénario mitoyen semi-réaliste de 584M.

# Scénario 2   

Ok, mettons qu'on ne fait pas chier les gens avant 2 millions, ça fait quoi?


::: {.cell}

```{.r .cell-code}
taxes2 <- function(x){
  case_when(
    x < 2e6 ~ 0,
    x < 10e6 ~   (x-2e6) *0.001,  # tops out at 8000
    x < 100e6  ~ 8000 + (x -10e6) * 0.01,  # tops out at 908000
    TRUE ~ 908000 + (x- 100e6) *0.015
  )
}
```
:::

::: {.cell}
::: {.cell-output-display}


```{=html}
<div id="ndusiqndfe" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:1080px;height:auto;">
<style>#ndusiqndfe table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#ndusiqndfe thead, #ndusiqndfe tbody, #ndusiqndfe tfoot, #ndusiqndfe tr, #ndusiqndfe td, #ndusiqndfe th {
  border-style: none;
}

#ndusiqndfe p {
  margin: 0;
  padding: 0;
}

#ndusiqndfe .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#ndusiqndfe .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#ndusiqndfe .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#ndusiqndfe .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#ndusiqndfe .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#ndusiqndfe .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ndusiqndfe .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#ndusiqndfe .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#ndusiqndfe .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#ndusiqndfe .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#ndusiqndfe .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#ndusiqndfe .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#ndusiqndfe .gt_spanner_row {
  border-bottom-style: hidden;
}

#ndusiqndfe .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#ndusiqndfe .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#ndusiqndfe .gt_from_md > :first-child {
  margin-top: 0;
}

#ndusiqndfe .gt_from_md > :last-child {
  margin-bottom: 0;
}

#ndusiqndfe .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#ndusiqndfe .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#ndusiqndfe .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#ndusiqndfe .gt_row_group_first td {
  border-top-width: 2px;
}

#ndusiqndfe .gt_row_group_first th {
  border-top-width: 2px;
}

#ndusiqndfe .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#ndusiqndfe .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#ndusiqndfe .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#ndusiqndfe .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ndusiqndfe .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#ndusiqndfe .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#ndusiqndfe .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#ndusiqndfe .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#ndusiqndfe .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ndusiqndfe .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#ndusiqndfe .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#ndusiqndfe .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#ndusiqndfe .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#ndusiqndfe .gt_left {
  text-align: left;
}

#ndusiqndfe .gt_center {
  text-align: center;
}

#ndusiqndfe .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#ndusiqndfe .gt_font_normal {
  font-weight: normal;
}

#ndusiqndfe .gt_font_bold {
  font-weight: bold;
}

#ndusiqndfe .gt_font_italic {
  font-style: italic;
}

#ndusiqndfe .gt_super {
  font-size: 65%;
}

#ndusiqndfe .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#ndusiqndfe .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#ndusiqndfe .gt_indent_1 {
  text-indent: 5px;
}

#ndusiqndfe .gt_indent_2 {
  text-indent: 10px;
}

#ndusiqndfe .gt_indent_3 {
  text-indent: 15px;
}

#ndusiqndfe .gt_indent_4 {
  text-indent: 20px;
}

#ndusiqndfe .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <caption>Données PUMF ESF Statcan pour le Québec 2019, calculs @coulsim</caption>
  <thead>
    <tr class="gt_heading">
      <td colspan="9" class="gt_heading gt_title gt_font_normal gt_bottom_border" style>Taxe sur la richesse récoltée selon le type de ménage (scénario cut-off 2M$)</td>
    </tr>
    
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre d'observations">Nombre d'observations</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre pondéré de ménages">Nombre pondéré de ménages</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario minimal">Nombre de ménages taxés dans le scénario minimal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario maximal">Nombre de ménages taxés dans le scénario maximal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario minimal">Taxe totale perçue dans le scénario minimal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario maximal">Taxe totale perçue dans le scénario maximal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario 50-50 ">Nombre de ménages taxés dans le scénario 50-50 </th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario 50-50">Taxe totale perçue dans le scénario 50-50</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub">Non déclaré</th>
<td headers="stub_1_1 nombre_observations" class="gt_row gt_right">63</td>
<td headers="stub_1_1 nombre_observations_ponderees" class="gt_row gt_right">66,791</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_min" class="gt_row gt_right">31,591</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_max" class="gt_row gt_right">34,918</td>
<td headers="stub_1_1 taxe_totale_scenario_min" class="gt_row gt_right">151,559,758</td>
<td headers="stub_1_1 taxe_totale_scenario_max" class="gt_row gt_right">467,570,456</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">33,254</td>
<td headers="stub_1_1 taxe_totale_scenario_50_50" class="gt_row gt_right">309,565,107</td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub">Autres types de famille</th>
<td headers="stub_1_2 nombre_observations" class="gt_row gt_right">233</td>
<td headers="stub_1_2 nombre_observations_ponderees" class="gt_row gt_right">486,400</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_min" class="gt_row gt_right">3,563</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_max" class="gt_row gt_right">33,906</td>
<td headers="stub_1_2 taxe_totale_scenario_min" class="gt_row gt_right">2,333,038</td>
<td headers="stub_1_2 taxe_totale_scenario_max" class="gt_row gt_right">29,165,117</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">18,734</td>
<td headers="stub_1_2 taxe_totale_scenario_50_50" class="gt_row gt_right">15,749,078</td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub">Couple, avec des enfants et famille monoparentale</th>
<td headers="stub_1_3 nombre_observations" class="gt_row gt_right">442</td>
<td headers="stub_1_3 nombre_observations_ponderees" class="gt_row gt_right">759,009</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_min" class="gt_row gt_right">1,211</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_max" class="gt_row gt_right">21,727</td>
<td headers="stub_1_3 taxe_totale_scenario_min" class="gt_row gt_right">1,202,293</td>
<td headers="stub_1_3 taxe_totale_scenario_max" class="gt_row gt_right">14,986,027</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">11,469</td>
<td headers="stub_1_3 taxe_totale_scenario_50_50" class="gt_row gt_right">8,094,160</td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub">Personne seule</th>
<td headers="stub_1_4 nombre_observations" class="gt_row gt_right">639</td>
<td headers="stub_1_4 nombre_observations_ponderees" class="gt_row gt_right">1,567,880</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_min" class="gt_row gt_right">21,712</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_max" class="gt_row gt_right">21,712</td>
<td headers="stub_1_4 taxe_totale_scenario_min" class="gt_row gt_right">14,238,078</td>
<td headers="stub_1_4 taxe_totale_scenario_max" class="gt_row gt_right">14,238,078</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">21,712</td>
<td headers="stub_1_4 taxe_totale_scenario_50_50" class="gt_row gt_right">14,238,078</td></tr>
    <tr><th id="stub_1_5" scope="row" class="gt_row gt_left gt_stub">Couple, sans enfant</th>
<td headers="stub_1_5 nombre_observations" class="gt_row gt_right">626</td>
<td headers="stub_1_5 nombre_observations_ponderees" class="gt_row gt_right">969,261</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_min" class="gt_row gt_right">8,184</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_max" class="gt_row gt_right">8,184</td>
<td headers="stub_1_5 taxe_totale_scenario_min" class="gt_row gt_right">8,339,843</td>
<td headers="stub_1_5 taxe_totale_scenario_max" class="gt_row gt_right">8,339,843</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">8,184</td>
<td headers="stub_1_5 taxe_totale_scenario_50_50" class="gt_row gt_right">8,339,843</td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">sum</th>
<td headers="grand_summary_stub_1 nombre_observations" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">2003</td>
<td headers="grand_summary_stub_1 nombre_observations_ponderees" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">3849341</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_min" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">66260.43</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_max" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">120446.3</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_min" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">177673010</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_max" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">534299522</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">93353.35</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_50_50" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">355986266</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::

Dans le scénario 50-50 du plan "cut-off à à 2 millions", on collecterait 355M.  C'est quand même 229M de moins (39%) que dans le scénario initial ( 584M).

Par contre, on fait chier 93 353 ménages au lieu de 330 864, une baisse de 71.7%


# Scenario 3  

Ok, est-ce qu'on peut retrouver un montant similaire au 584M initial en augmentant le taux d'imposition entre 2M et 10 M à 0.2% au lieu de 0.1% ?

::: {.cell}

```{.r .cell-code}
taxes3 <- function(x){
  case_when(
    x < 2e6 ~ 0,
    x < 10e6 ~   (x-2e6) *0.002,  # tops out at 16000
    x < 100e6  ~ 16000 + (x -10e6) * 0.01,  # tops out at 916000
    TRUE ~ 916000 + (x- 100e6) *0.015
  )
}
```
:::

::: {.cell}
::: {.cell-output-display}


```{=html}
<div id="qxtjabqsfn" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:1080px;height:auto;">
<style>#qxtjabqsfn table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#qxtjabqsfn thead, #qxtjabqsfn tbody, #qxtjabqsfn tfoot, #qxtjabqsfn tr, #qxtjabqsfn td, #qxtjabqsfn th {
  border-style: none;
}

#qxtjabqsfn p {
  margin: 0;
  padding: 0;
}

#qxtjabqsfn .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#qxtjabqsfn .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#qxtjabqsfn .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#qxtjabqsfn .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#qxtjabqsfn .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#qxtjabqsfn .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#qxtjabqsfn .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#qxtjabqsfn .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#qxtjabqsfn .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#qxtjabqsfn .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#qxtjabqsfn .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#qxtjabqsfn .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#qxtjabqsfn .gt_spanner_row {
  border-bottom-style: hidden;
}

#qxtjabqsfn .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#qxtjabqsfn .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#qxtjabqsfn .gt_from_md > :first-child {
  margin-top: 0;
}

#qxtjabqsfn .gt_from_md > :last-child {
  margin-bottom: 0;
}

#qxtjabqsfn .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#qxtjabqsfn .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#qxtjabqsfn .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#qxtjabqsfn .gt_row_group_first td {
  border-top-width: 2px;
}

#qxtjabqsfn .gt_row_group_first th {
  border-top-width: 2px;
}

#qxtjabqsfn .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#qxtjabqsfn .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#qxtjabqsfn .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#qxtjabqsfn .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#qxtjabqsfn .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#qxtjabqsfn .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#qxtjabqsfn .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#qxtjabqsfn .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#qxtjabqsfn .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#qxtjabqsfn .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#qxtjabqsfn .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#qxtjabqsfn .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#qxtjabqsfn .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#qxtjabqsfn .gt_left {
  text-align: left;
}

#qxtjabqsfn .gt_center {
  text-align: center;
}

#qxtjabqsfn .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#qxtjabqsfn .gt_font_normal {
  font-weight: normal;
}

#qxtjabqsfn .gt_font_bold {
  font-weight: bold;
}

#qxtjabqsfn .gt_font_italic {
  font-style: italic;
}

#qxtjabqsfn .gt_super {
  font-size: 65%;
}

#qxtjabqsfn .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#qxtjabqsfn .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#qxtjabqsfn .gt_indent_1 {
  text-indent: 5px;
}

#qxtjabqsfn .gt_indent_2 {
  text-indent: 10px;
}

#qxtjabqsfn .gt_indent_3 {
  text-indent: 15px;
}

#qxtjabqsfn .gt_indent_4 {
  text-indent: 20px;
}

#qxtjabqsfn .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <caption>Données PUMF ESF Statcan pour le Québec 2019, calculs @coulsim</caption>
  <thead>
    <tr class="gt_heading">
      <td colspan="9" class="gt_heading gt_title gt_font_normal gt_bottom_border" style>Taxe sur la richesse récoltée selon le type de ménage (scénario 3: cut-off 2M$, taux de 0.2% entre 2M et 10M)</td>
    </tr>
    
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre d'observations">Nombre d'observations</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre pondéré de ménages">Nombre pondéré de ménages</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario minimal">Nombre de ménages taxés dans le scénario minimal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario maximal">Nombre de ménages taxés dans le scénario maximal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario minimal">Taxe totale perçue dans le scénario minimal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario maximal">Taxe totale perçue dans le scénario maximal</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Nombre de ménages taxés dans le scénario 50-50">Nombre de ménages taxés dans le scénario 50-50</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Taxe totale perçue dans le scénario 50-50">Taxe totale perçue dans le scénario 50-50</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub">Non déclaré</th>
<td headers="stub_1_1 nombre_observations" class="gt_row gt_right">63</td>
<td headers="stub_1_1 nombre_observations_ponderees" class="gt_row gt_right">66,791</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_min" class="gt_row gt_right">31,591</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_max" class="gt_row gt_right">34,918</td>
<td headers="stub_1_1 taxe_totale_scenario_min" class="gt_row gt_right">303,119,517</td>
<td headers="stub_1_1 taxe_totale_scenario_max" class="gt_row gt_right">658,380,765</td>
<td headers="stub_1_1 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">33,254</td>
<td headers="stub_1_1 taxe_totale_scenario_50_50" class="gt_row gt_right">480,750,141</td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub">Autres types de famille</th>
<td headers="stub_1_2 nombre_observations" class="gt_row gt_right">233</td>
<td headers="stub_1_2 nombre_observations_ponderees" class="gt_row gt_right">486,400</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_min" class="gt_row gt_right">3,563</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_max" class="gt_row gt_right">33,906</td>
<td headers="stub_1_2 taxe_totale_scenario_min" class="gt_row gt_right">4,666,076</td>
<td headers="stub_1_2 taxe_totale_scenario_max" class="gt_row gt_right">58,330,235</td>
<td headers="stub_1_2 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">18,734</td>
<td headers="stub_1_2 taxe_totale_scenario_50_50" class="gt_row gt_right">31,498,155</td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub">Couple, avec des enfants et famille monoparentale</th>
<td headers="stub_1_3 nombre_observations" class="gt_row gt_right">442</td>
<td headers="stub_1_3 nombre_observations_ponderees" class="gt_row gt_right">759,009</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_min" class="gt_row gt_right">1,211</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_max" class="gt_row gt_right">21,727</td>
<td headers="stub_1_3 taxe_totale_scenario_min" class="gt_row gt_right">2,404,586</td>
<td headers="stub_1_3 taxe_totale_scenario_max" class="gt_row gt_right">29,972,054</td>
<td headers="stub_1_3 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">11,469</td>
<td headers="stub_1_3 taxe_totale_scenario_50_50" class="gt_row gt_right">16,188,320</td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub">Personne seule</th>
<td headers="stub_1_4 nombre_observations" class="gt_row gt_right">639</td>
<td headers="stub_1_4 nombre_observations_ponderees" class="gt_row gt_right">1,567,880</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_min" class="gt_row gt_right">21,712</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_max" class="gt_row gt_right">21,712</td>
<td headers="stub_1_4 taxe_totale_scenario_min" class="gt_row gt_right">28,476,156</td>
<td headers="stub_1_4 taxe_totale_scenario_max" class="gt_row gt_right">28,476,156</td>
<td headers="stub_1_4 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">21,712</td>
<td headers="stub_1_4 taxe_totale_scenario_50_50" class="gt_row gt_right">28,476,156</td></tr>
    <tr><th id="stub_1_5" scope="row" class="gt_row gt_left gt_stub">Couple, sans enfant</th>
<td headers="stub_1_5 nombre_observations" class="gt_row gt_right">626</td>
<td headers="stub_1_5 nombre_observations_ponderees" class="gt_row gt_right">969,261</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_min" class="gt_row gt_right">8,184</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_max" class="gt_row gt_right">8,184</td>
<td headers="stub_1_5 taxe_totale_scenario_min" class="gt_row gt_right">16,679,686</td>
<td headers="stub_1_5 taxe_totale_scenario_max" class="gt_row gt_right">16,679,686</td>
<td headers="stub_1_5 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right">8,184</td>
<td headers="stub_1_5 taxe_totale_scenario_50_50" class="gt_row gt_right">16,679,686</td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">sum</th>
<td headers="grand_summary_stub_1 nombre_observations" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">2003</td>
<td headers="grand_summary_stub_1 nombre_observations_ponderees" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">3849341</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_min" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">66260.43</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_max" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">120446.3</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_min" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">355346020</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_max" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">791838896</td>
<td headers="grand_summary_stub_1 nombre_menages_taxes_scenario_50_50" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">93353.35</td>
<td headers="grand_summary_stub_1 taxe_totale_scenario_50_50" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">573592458</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::


573M ! 
C'est pas mal proche du 584M initial, et ça embête seulement les gens doublement millionnaire en leur demande de payer 2000$ par millions à partir du 2e (et 10 000\$ par million à partir du 10e)


# Conclusion   

Les données du PUMF de l'Enquête sur la Sécurité Financière de 2019 nous permettent de savoir que la taxe sur la richesse aurait rapporté entre 383M et 784M en utilisant les règles énoncées par QS.  Il s'agit de deux scénarios extrêmes, où l'on suppose que toutes les familles dans les catégorie "Non déclaré", "Autres types de famille" et "Couple, avec des enfants et famille monoparentale" sont composé soit de personnes seules (scénario impôt maximal) ou de couples (scénario impôt minimal) 

Un scénario mitoyen semi-réaliste où la moitié de ces ménages seraient composé de personnes seules et l'autre moitié de couple permettrait de récolter **584M** auprès de **330,864** des 3,849,341 ménages  du Québec (8.59%).

Ce pourcentage est beaucoup plus élevé que ceux que nous avions vu hier quand j'avais trouvé 5.2% pour les personnes seules et de 6.8% pour les couples sans enfants.  C'est parce qu'hier je ne m'étais pas intéressés aux familles où le nombre d'adultes était inconu.  Dans les familles "non déclarés", ce sont **64%** de 66 000 ménages qui paient dans le scénario 50-50.  Pour les "autres types de familles ce sont **16.9%** de 486 400 ménages.  Enfin, pour les ménages composés de "couples avec enfants et famille monoparentale", si on suppose que la moitié ne comporte qu'un adulte, on arrive à 7.5% des 759 009 ménages.  Ce dernier chiffre est probablement surestimé, car j'ai supposé 50% de familles monoparentales alors que la [réalité est plus proche de 29.5%](https://msss.gouv.qc.ca/professionnels/statistiques-donnees-sante-bien-etre/statistiques-de-sante-et-de-bien-etre-selon-le-sexe-volet-national/familles-monoparentales/)


Nous avons ensuite créé un deuxième ensemble de règles, le scénario #2, où ce sont les 2 premiers millions qui seraient exonérés plutôt que seulement le premier.  Sous cet ensemble de règles,  on ne collectait que **355 millions** dans le scénario 50-50, une baisse de  229M (39%) par rapport à l'ensemble de règles initial.  Par contre, on embêtait seulement **93 353 ménages**  au lieu de 330 864, une baisse de 71.7%.  Embêter 2.4% des ménages au lieu de 8.59% des ménages me parait plus raisonnable, mais il faudrait quand même retrouver ces 229 millions.

Nous avons donc créé un  troisième ensemble de règles, le scénario #3, où les 2 premiers millions sont exonérés mais où le taux de taxation sur l'avoir net est de 2000\$ par millions plutôt que de 1000\$ par million entre 2M et 10M. Sous cet ensemble de règles, on collecte alors **573 millions** auprès des mêmes **93 353 ménages** que dans scénario #2.

Conclusion: le troisième ensemble de règle permettrait de récolter presque autant d'argent que celui proposé par QS (573M vs 584M) et on pourrait dire "We are the 97.5%ish" au lieu de "We are the 91.4%"





