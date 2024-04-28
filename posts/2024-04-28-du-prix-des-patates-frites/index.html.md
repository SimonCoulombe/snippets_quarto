---
title: "Peut-on se fier à Sylvain Charlebois?"
description: |
  iiiiish
author: Simon Coulombe
date: 2024-04-28
categories: []
lang: fr
---


::: {.cell}

:::



:::{.callout-tip}
## Pourquoi est-ce qu'on est ici?  

Petite chicane d'économistes sur linkedin tantôt à propos d'[un article dans la presse d'un prof de dalhousie qui parle de bouffe](https://www.lapresse.ca/affaires/chroniques/2024-04-18/panier-d-epicerie/peut-on-vraiment-se-fier-a-statistique-canada.php).  Il compare son ipc qu'il a calculé personnellement à celui de statistique canada et évidemment toute différence entre son chiffre et celui par publié par statcan est une erreur de statcan.  Tout ça sans partager sa méthodologie et ses données.   

Avant de critiquer les chiffres de statcan, je me suis dit que ce serait fun de voir quels sont les chiffres de statcan directement de la source.   Pas facile de savoir exactement où, car l'article parle simplement de source "statistique canada".  

Fak, je me suis attaqué à la liste des tableaux de statcan à l'aide du toujours excellent package {cansim} de @vb_jens afin, je l'espère de trouver la source utilisée.  

:::   


Voici les noms de quelques tableux prometteurs de Statcan:  

::: {.cell}
::: {.cell-output-display}


|cansim_table_number |cube_title_fr                                                                    |
|:-------------------|:--------------------------------------------------------------------------------|
|18-10-0001          |Prix de détail moyens mensuel, essence et mazout, par géographie                 |
|18-10-0002          |Prix de détail moyens mensuels pour les aliments et autres produits sélectionnés |
|18-10-0245          |Prix de détail moyens mensuels pour certains produits                            |


:::
:::



Note: le tableau "18-10-0004" était prometteur aussi, mais n'a pas de cantaloupe.   

J'ai regardé ces 4 tableaux et le seul qui contenait le mot "cantalope" est [18-10-0245](https://www150.statcan.gc.ca/t1/tbl1/fr/tv.action?pid=1810024501&pickMembers%5B0%5D=1.11&request_locale=fr).  J'imagine que c'est à celui-là que fait référence l'article de la presse.  Ça a du sens, parce que le "prix de détail" c'est ce qu'un citoyen peut mesurer et à quoi il peut se comparer.  

Bref, j'ai downloadé les chiffres, j'ai pitché ça dans un tableau.   Voici l'évolution des prix des aliments de février 2023 à février 2024 au Canada et au Québec selon Statcan.  


Ça "fitte" vraiment pas avec les chiffres dans l'article de La presse.  PAr exemple, pour les avocats, je vois +9.1% (Canada) ou -7.8%(Québec), alors que le chiffre attribué à Statcan dans la presse est de -4%.

Possible que j'ai pas regardé le bon vecteur chez statcan.  Possible aussi que les calculs en face ne soient pas bons.   

a+





::: {.cell .column-screen}
::: {.cell-output-display}


```{=html}
<div id="yyzobplzpw" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#yyzobplzpw table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#yyzobplzpw thead, #yyzobplzpw tbody, #yyzobplzpw tfoot, #yyzobplzpw tr, #yyzobplzpw td, #yyzobplzpw th {
  border-style: none;
}

#yyzobplzpw p {
  margin: 0;
  padding: 0;
}

#yyzobplzpw .gt_table {
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

#yyzobplzpw .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#yyzobplzpw .gt_title {
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

#yyzobplzpw .gt_subtitle {
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

#yyzobplzpw .gt_heading {
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

#yyzobplzpw .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#yyzobplzpw .gt_col_headings {
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

#yyzobplzpw .gt_col_heading {
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

#yyzobplzpw .gt_column_spanner_outer {
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

#yyzobplzpw .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#yyzobplzpw .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#yyzobplzpw .gt_column_spanner {
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

#yyzobplzpw .gt_spanner_row {
  border-bottom-style: hidden;
}

#yyzobplzpw .gt_group_heading {
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

#yyzobplzpw .gt_empty_group_heading {
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

#yyzobplzpw .gt_from_md > :first-child {
  margin-top: 0;
}

#yyzobplzpw .gt_from_md > :last-child {
  margin-bottom: 0;
}

#yyzobplzpw .gt_row {
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

#yyzobplzpw .gt_stub {
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

#yyzobplzpw .gt_stub_row_group {
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

#yyzobplzpw .gt_row_group_first td {
  border-top-width: 2px;
}

#yyzobplzpw .gt_row_group_first th {
  border-top-width: 2px;
}

#yyzobplzpw .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#yyzobplzpw .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#yyzobplzpw .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#yyzobplzpw .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#yyzobplzpw .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#yyzobplzpw .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#yyzobplzpw .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#yyzobplzpw .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#yyzobplzpw .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#yyzobplzpw .gt_footnotes {
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

#yyzobplzpw .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#yyzobplzpw .gt_sourcenotes {
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

#yyzobplzpw .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#yyzobplzpw .gt_left {
  text-align: left;
}

#yyzobplzpw .gt_center {
  text-align: center;
}

#yyzobplzpw .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#yyzobplzpw .gt_font_normal {
  font-weight: normal;
}

#yyzobplzpw .gt_font_bold {
  font-weight: bold;
}

#yyzobplzpw .gt_font_italic {
  font-style: italic;
}

#yyzobplzpw .gt_super {
  font-size: 65%;
}

#yyzobplzpw .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#yyzobplzpw .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#yyzobplzpw .gt_indent_1 {
  text-indent: 5px;
}

#yyzobplzpw .gt_indent_2 {
  text-indent: 10px;
}

#yyzobplzpw .gt_indent_3 {
  text-indent: 15px;
}

#yyzobplzpw .gt_indent_4 {
  text-indent: 20px;
}

#yyzobplzpw .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="7" class="gt_heading gt_title gt_font_normal" style>Évolution du prix de détail moyens mensuels pour certains produits</td>
    </tr>
    <tr class="gt_heading">
      <td colspan="7" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style>Mais quel source de données Sylvain Charlebois a-t-il utilisé? </td>
    </tr>
    <tr class="gt_col_headings gt_spanner_row">
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="2" colspan="1" scope="col" id="produits">produits</th>
      <th class="gt_center gt_columns_top_border gt_column_spanner_outer" rowspan="1" colspan="3" scope="colgroup" id="Canada">
        <span class="gt_column_spanner">Canada</span>
      </th>
      <th class="gt_center gt_columns_top_border gt_column_spanner_outer" rowspan="1" colspan="3" scope="colgroup" id="Québec">
        <span class="gt_column_spanner">Québec</span>
      </th>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Prix Février 2023">Prix Février 2023</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Prix Février 2024">Prix Février 2024</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Différence en %">Différence en %</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Prix Février 2023">Prix Février 2023</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Prix Février 2024">Prix Février 2024</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Différence en %">Différence en %</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="produits" class="gt_row gt_center">Avocat, unité</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$1.65</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$1.80</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">9.1%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$1.66</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$1.53</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−7.8%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Brocoli surgelé, 500 grammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$3.87</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$3.98</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">2.8%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$3.68</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$4.13</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">12.2%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Brocoli, unité</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$3.11</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$2.27</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−27.0%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$3.06</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$2.01</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−34.3%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Café torréfié ou moulu, 340 grammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$6.58</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$6.38</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−3.0%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$6.40</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$6.57</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">2.7%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Cantaloup, unité</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$3.86</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$3.27</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−15.3%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$3.82</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$3.11</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−18.6%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Fraises surgelé, 600 grammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$5.36</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$4.83</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−9.9%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$5.25</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$4.74</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−9.7%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Fraises, 454 grammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$4.49</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$3.89</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−13.4%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$4.31</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$3.39</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−21.3%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Houmous, 227 grammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$3.85</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$3.66</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−4.9%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$3.76</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$3.55</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−5.6%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Jus d’orange, 2 litres</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$4.23</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$5.26</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">24.3%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$4.55</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$5.41</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">18.9%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Oignons, 1,36 kilogrammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$4.37</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$4.72</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">8.0%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$3.53</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$4.38</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">24.1%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Oignons, par kilogramme</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$5.41</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$5.64</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">4.3%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$4.48</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$5.75</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">28.3%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Oranges, 1,36 kilogrammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$5.28</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$4.77</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−9.7%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$5.06</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$4.40</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−13.0%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Oranges, par kilogramme</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$3.61</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$3.17</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−12.2%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$6.32</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$3.55</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−43.8%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Pâtes sèches ou fraîches, 500 grammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$3.67</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$3.08</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−16.1%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$3.56</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$3.23</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−9.3%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Poire en conserve, 398 millilitres</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$2.69</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$2.73</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">1.5%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$2.92</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$2.78</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−4.8%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Poires, par kilogramme</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$6.02</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$5.69</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−5.5%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$6.60</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$6.02</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−8.8%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Pommes de terre frites surgelées, 750 grammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$2.99</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$3.58</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">19.7%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$3.19</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$3.69</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">15.7%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Pommes de terre, 4,54 kilogrammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$4.83</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$4.34</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−10.1%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$4.10</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$3.99</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−2.7%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Pommes de terre, par kilogramme</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$4.76</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$4.86</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">2.1%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$4.71</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$4.61</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−2.1%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Saumon en conserve, 213 grammes</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$4.42</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$4.54</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">2.7%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$4.70</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$4.67</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−0.6%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Saumon, par kilogramme</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$28.32</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$26.37</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−6.9%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$28.34</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$25.63</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−9.6%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Soupe en conserve, 284 millilitres</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$1.63</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$1.32</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">−19.0%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$1.37</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$1.27</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">−7.3%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Tomates en conserve, 796 millilitres</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$1.88</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$2.03</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">8.0%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$1.74</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$2.04</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">17.2%</td></tr>
    <tr><td headers="produits" class="gt_row gt_center">Tomates, par kilogramme</td>
<td headers="prix_an_2023_geo_Canada" class="gt_row gt_right">$5.85</td>
<td headers="prix_an_2024_geo_Canada" class="gt_row gt_right">$5.94</td>
<td headers="pct_diff_geo_Canada" class="gt_row gt_right">1.5%</td>
<td headers="prix_an_2023_geo_Québec" class="gt_row gt_right">$6.80</td>
<td headers="prix_an_2024_geo_Québec" class="gt_row gt_right">$6.88</td>
<td headers="pct_diff_geo_Québec" class="gt_row gt_right">1.2%</td></tr>
  </tbody>
  
  <tfoot class="gt_footnotes">
    <tr>
      <td class="gt_footnote" colspan="7"> Source : Statistique Canada, Tableau 18-10-0245, via package {cansim} par @vb_jens </td>
    </tr>
  </tfoot>
</table>
</div>
```


:::
:::





![](charlebois.png)

