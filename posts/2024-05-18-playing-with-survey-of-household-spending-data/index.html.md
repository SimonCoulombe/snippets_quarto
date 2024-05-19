---
title: "Enquête sur les dépenses des ménages"
description: "Devinez quelles catégories ont moins de dépense en 2021 qu'en 2010 au Québec"
author: Simon Coulombe
date: 2024-05-18
categories: []
lang: fr
---



Pourquoi on est ici déjà?

J'ai été "déclenché" par un reel stupide sur facebook qui ne citait pas ses sources.  Ils disaient que ça coûterait peut-être moins cher d'habiter dans un resort tout-inclus parce que la vie au Canada pour une personne seule coûte en moyenne 4000$ par mois.   

J'ai regardé rapidement les tableaux de "Enquête sur les dépenses des ménages" et j'Ai vu que le *ménage* canadien moyen dépensait 92 000\$ par année (ou 7 666 \$ par mois).  C'est pas trop off si on suppose une taille des ménages moyenne de 2, mais j'Ai pas regardé très longemps pour trouver les données pour les personnes seules.   

Pendant que j'y étais, j'ai vu une catégorie où les ménages canadiens dépensaient beaucoup moins en 2021 qu'en 2010 et ça a piqué ma curiosité.  J'ai donc téléchargé toutes les données pour essayer d'en trouver d'autres.  

Hang on for code on how to access the "Survey of Household Spending Data"  et connaître la catégorie en question.   :)   

note: gros code dégueux fait avant d'aller me coucher. bien sûr, ce devrait être des fonctions au lieu de copy-paste, mais c'est ça ou rien.  



::: {.cell}

:::


# Download les tables pour  2010, 2019 et 2021  au Québec    

Merci package Cansim de Jens Von Bergmann :)


::: {.cell}

:::

# profondeur 0   

Les dépenses sont ventilées par catégories, et ensuite chaque catégorie  est ventilées parmi ses  "enfants".  Voici les dépenses à la profondeur 0 (total) pour les 3 années retenues:  
Augmentation de 29.23% en 11 ans de 2010 à 2021 au Québec.  

::: {.cell .column-screen-inset}

````{.cell-code}
```{{r}}
#| column: screen-inset
tableau_wide %>% 
  filter(profondeur== 0) %>%
  select(-profondeur, -last_profondeur) %>% 
  gt::gt() %>%
  gt::cols_label(.list= setNames(as.list(names_with_spaces),names(tableau_wide%>% select(-profondeur, -last_profondeur)) )) %>%  
  fmt_number(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), decimals = 0) %>%
  fmt_percent(columns = c(diff_rel2019, diff_rel2021)) %>% 
  gt::grand_summary_rows(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), 
                         fns = list(Total ~ sum(.,na.rm = TRUE)) ,
                         fmt = ~fmt_number(., decimals = 0)) %>%
  gt_plt_bar(column = diff_rel2019, keep_column = TRUE, color = cerulean_blue )
```
````

::: {.cell-output-display}


```{=html}
<div id="uydzarejfr" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#uydzarejfr table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#uydzarejfr thead, #uydzarejfr tbody, #uydzarejfr tfoot, #uydzarejfr tr, #uydzarejfr td, #uydzarejfr th {
  border-style: none;
}

#uydzarejfr p {
  margin: 0;
  padding: 0;
}

#uydzarejfr .gt_table {
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

#uydzarejfr .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#uydzarejfr .gt_title {
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

#uydzarejfr .gt_subtitle {
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

#uydzarejfr .gt_heading {
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

#uydzarejfr .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#uydzarejfr .gt_col_headings {
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

#uydzarejfr .gt_col_heading {
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

#uydzarejfr .gt_column_spanner_outer {
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

#uydzarejfr .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#uydzarejfr .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#uydzarejfr .gt_column_spanner {
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

#uydzarejfr .gt_spanner_row {
  border-bottom-style: hidden;
}

#uydzarejfr .gt_group_heading {
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

#uydzarejfr .gt_empty_group_heading {
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

#uydzarejfr .gt_from_md > :first-child {
  margin-top: 0;
}

#uydzarejfr .gt_from_md > :last-child {
  margin-bottom: 0;
}

#uydzarejfr .gt_row {
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

#uydzarejfr .gt_stub {
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

#uydzarejfr .gt_stub_row_group {
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

#uydzarejfr .gt_row_group_first td {
  border-top-width: 2px;
}

#uydzarejfr .gt_row_group_first th {
  border-top-width: 2px;
}

#uydzarejfr .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#uydzarejfr .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#uydzarejfr .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#uydzarejfr .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#uydzarejfr .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#uydzarejfr .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#uydzarejfr .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#uydzarejfr .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#uydzarejfr .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#uydzarejfr .gt_footnotes {
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

#uydzarejfr .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#uydzarejfr .gt_sourcenotes {
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

#uydzarejfr .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#uydzarejfr .gt_left {
  text-align: left;
}

#uydzarejfr .gt_center {
  text-align: center;
}

#uydzarejfr .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#uydzarejfr .gt_font_normal {
  font-weight: normal;
}

#uydzarejfr .gt_font_bold {
  font-weight: bold;
}

#uydzarejfr .gt_font_italic {
  font-style: italic;
}

#uydzarejfr .gt_super {
  font-size: 65%;
}

#uydzarejfr .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#uydzarejfr .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#uydzarejfr .gt_indent_1 {
  text-indent: 5px;
}

#uydzarejfr .gt_indent_2 {
  text-indent: 10px;
}

#uydzarejfr .gt_indent_3 {
  text-indent: 15px;
}

#uydzarejfr .gt_indent_4 {
  text-indent: 20px;
}

#uydzarejfr .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="hierarchie pour depenses des menages categories de niveau sommaire">hierarchie pour depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="depenses des menages categories de niveau sommaire">depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2010">an2010</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2019">an2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2021">an2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2019">diff abs2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2021">diff abs2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2019">diff rel2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2021">diff rel2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="diff_rel2019">diff_rel2019</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1</td>
<td headers="stub_1_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dépenses totales</td>
<td headers="stub_1_1 an2010" class="gt_row gt_right">62,257</td>
<td headers="stub_1_1 an2019" class="gt_row gt_right">79,639</td>
<td headers="stub_1_1 an2021" class="gt_row gt_right">80,452</td>
<td headers="stub_1_1 diff_abs2019" class="gt_row gt_right">17,382</td>
<td headers="stub_1_1 diff_abs2021" class="gt_row gt_right">18,195</td>
<td headers="stub_1_1 diff_rel2019" class="gt_row gt_right">27.92%</td>
<td headers="stub_1_1 diff_rel2021" class="gt_row gt_right">29.23%</td>
<td headers="stub_1_1 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.02' y='0.89' width='98.37' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='5.02' y1='14.17' x2='5.02' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">Total</th>
<td headers="grand_summary_stub_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 an2010" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">62,257</td>
<td headers="grand_summary_stub_1 an2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">79,639</td>
<td headers="grand_summary_stub_1 an2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">80,452</td>
<td headers="grand_summary_stub_1 diff_abs2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">17,382</td>
<td headers="grand_summary_stub_1 diff_abs2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">18,195</td>
<td headers="grand_summary_stub_1 diff_rel2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 diff_rel2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 DUPE_COLUMN_PLT" class="gt_row gt_left gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::


# profondeur 1     

Quand on ventile un peu (profondeur = 1 ), on peut séparer les dépenses courantes des impôts et des assurances/pensions ainsi que des cadeaux.   

Première réaction de votre dévoué serviteur:  **WTF IMPOT SUR LE REVENU + 61%**  !!!  

Il a suffit de quelques secondes et d'une note de bas de page pour comprendre que les Québécois ne sont pas soudainment pas plus taxés qu'avant.  C'est juste que les primes d'Assurance-maladie provinciales (médicament?) sont passées de dépenses de santé à dépenses d'impôt:  

```
Note de bas de page 8
https://www150.statcan.gc.ca/t1/tbl1/fr/tv.action?pid=1110022201&request_locale=fr
À partir de 2014, les estimations de dépenses pour les primes d'assurance-maladie provinciale sont incluses dans l'impôt sur le revenu. Ces estimations sont basées sur de l'information provenant des données d'impôt des particuliers (T1). Précédemment, les primes d'assurance-maladie provinciale étaient incluses dans les dépenses de soins de santé
```


::: {.cell .column-screen-inset}

````{.cell-code}
```{{r}}
#| column: screen-inset
tableau_wide %>% 
  filter(profondeur== 1 ) %>%
  select(-profondeur, -last_profondeur) %>% 
  gt::gt() %>%
  gt::cols_label(.list= setNames(as.list(names_with_spaces),names(tableau_wide%>% select(-profondeur, -last_profondeur)) )) %>%  ###  this is clever af simon!! quick tip to replace all "_" with " " in the column labels
  fmt_number(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), decimals = 0) %>%
  fmt_percent(columns = c(diff_rel2019, diff_rel2021)) %>% 
  gt::grand_summary_rows(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), 
                         fns = list(Total ~ sum(.,na.rm = TRUE)) ,
                         fmt = ~fmt_number(., decimals = 0)) %>%
  gt_plt_bar(column = diff_rel2019, keep_column = TRUE, color = cerulean_blue ) %>% 
  gt::sub_missing(missing_text = "-")
```
````

::: {.cell-output-display}


```{=html}
<div id="kqvwrnzaox" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#kqvwrnzaox table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#kqvwrnzaox thead, #kqvwrnzaox tbody, #kqvwrnzaox tfoot, #kqvwrnzaox tr, #kqvwrnzaox td, #kqvwrnzaox th {
  border-style: none;
}

#kqvwrnzaox p {
  margin: 0;
  padding: 0;
}

#kqvwrnzaox .gt_table {
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

#kqvwrnzaox .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#kqvwrnzaox .gt_title {
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

#kqvwrnzaox .gt_subtitle {
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

#kqvwrnzaox .gt_heading {
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

#kqvwrnzaox .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#kqvwrnzaox .gt_col_headings {
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

#kqvwrnzaox .gt_col_heading {
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

#kqvwrnzaox .gt_column_spanner_outer {
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

#kqvwrnzaox .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#kqvwrnzaox .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#kqvwrnzaox .gt_column_spanner {
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

#kqvwrnzaox .gt_spanner_row {
  border-bottom-style: hidden;
}

#kqvwrnzaox .gt_group_heading {
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

#kqvwrnzaox .gt_empty_group_heading {
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

#kqvwrnzaox .gt_from_md > :first-child {
  margin-top: 0;
}

#kqvwrnzaox .gt_from_md > :last-child {
  margin-bottom: 0;
}

#kqvwrnzaox .gt_row {
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

#kqvwrnzaox .gt_stub {
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

#kqvwrnzaox .gt_stub_row_group {
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

#kqvwrnzaox .gt_row_group_first td {
  border-top-width: 2px;
}

#kqvwrnzaox .gt_row_group_first th {
  border-top-width: 2px;
}

#kqvwrnzaox .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#kqvwrnzaox .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#kqvwrnzaox .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#kqvwrnzaox .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#kqvwrnzaox .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#kqvwrnzaox .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#kqvwrnzaox .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#kqvwrnzaox .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#kqvwrnzaox .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#kqvwrnzaox .gt_footnotes {
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

#kqvwrnzaox .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#kqvwrnzaox .gt_sourcenotes {
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

#kqvwrnzaox .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#kqvwrnzaox .gt_left {
  text-align: left;
}

#kqvwrnzaox .gt_center {
  text-align: center;
}

#kqvwrnzaox .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#kqvwrnzaox .gt_font_normal {
  font-weight: normal;
}

#kqvwrnzaox .gt_font_bold {
  font-weight: bold;
}

#kqvwrnzaox .gt_font_italic {
  font-style: italic;
}

#kqvwrnzaox .gt_super {
  font-size: 65%;
}

#kqvwrnzaox .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#kqvwrnzaox .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#kqvwrnzaox .gt_indent_1 {
  text-indent: 5px;
}

#kqvwrnzaox .gt_indent_2 {
  text-indent: 10px;
}

#kqvwrnzaox .gt_indent_3 {
  text-indent: 15px;
}

#kqvwrnzaox .gt_indent_4 {
  text-indent: 20px;
}

#kqvwrnzaox .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="hierarchie pour depenses des menages categories de niveau sommaire">hierarchie pour depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="depenses des menages categories de niveau sommaire">depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2010">an2010</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2019">an2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2021">an2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2019">diff abs2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2021">diff abs2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2019">diff rel2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2021">diff rel2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="diff_rel2019">diff_rel2019</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2</td>
<td headers="stub_1_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Consommation courante totale</td>
<td headers="stub_1_1 an2010" class="gt_row gt_right">47,752</td>
<td headers="stub_1_1 an2019" class="gt_row gt_right">58,208</td>
<td headers="stub_1_1 an2021" class="gt_row gt_right">57,889</td>
<td headers="stub_1_1 diff_abs2019" class="gt_row gt_right">10,456</td>
<td headers="stub_1_1 diff_abs2021" class="gt_row gt_right">10,137</td>
<td headers="stub_1_1 diff_rel2019" class="gt_row gt_right">21.90%</td>
<td headers="stub_1_1 diff_rel2021" class="gt_row gt_right">21.23%</td>
<td headers="stub_1_1 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.02' y='0.89' width='34.26' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='5.02' y1='14.17' x2='5.02' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_2 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.40</td>
<td headers="stub_1_2 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Impôts sur le revenu</td>
<td headers="stub_1_2 an2010" class="gt_row gt_right">10,130</td>
<td headers="stub_1_2 an2019" class="gt_row gt_right">15,030</td>
<td headers="stub_1_2 an2021" class="gt_row gt_right">16,342</td>
<td headers="stub_1_2 diff_abs2019" class="gt_row gt_right">4,900</td>
<td headers="stub_1_2 diff_abs2021" class="gt_row gt_right">6,212</td>
<td headers="stub_1_2 diff_rel2019" class="gt_row gt_right">48.37%</td>
<td headers="stub_1_2 diff_rel2021" class="gt_row gt_right">61.32%</td>
<td headers="stub_1_2 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.02' y='0.89' width='75.69' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='5.02' y1='14.17' x2='5.02' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_3 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41</td>
<td headers="stub_1_3 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Paiements d'assurance individuelle et cotisations à des régimes de pension de retraite</td>
<td headers="stub_1_3 an2010" class="gt_row gt_right">3,629</td>
<td headers="stub_1_3 an2019" class="gt_row gt_right">5,186</td>
<td headers="stub_1_3 an2021" class="gt_row gt_right">5,422</td>
<td headers="stub_1_3 diff_abs2019" class="gt_row gt_right">1,557</td>
<td headers="stub_1_3 diff_abs2021" class="gt_row gt_right">1,793</td>
<td headers="stub_1_3 diff_rel2019" class="gt_row gt_right">42.90%</td>
<td headers="stub_1_3 diff_rel2021" class="gt_row gt_right">49.41%</td>
<td headers="stub_1_3 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.02' y='0.89' width='67.13' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='5.02' y1='14.17' x2='5.02' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_4 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42</td>
<td headers="stub_1_4 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux en argent, pensions alimentaires et dons de bienfaisance</td>
<td headers="stub_1_4 an2010" class="gt_row gt_right">746</td>
<td headers="stub_1_4 an2019" class="gt_row gt_right">1,215</td>
<td headers="stub_1_4 an2021" class="gt_row gt_right">800</td>
<td headers="stub_1_4 diff_abs2019" class="gt_row gt_right">469</td>
<td headers="stub_1_4 diff_abs2021" class="gt_row gt_right">54</td>
<td headers="stub_1_4 diff_rel2019" class="gt_row gt_right">62.87%</td>
<td headers="stub_1_4 diff_rel2021" class="gt_row gt_right">7.24%</td>
<td headers="stub_1_4 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.02' y='0.89' width='98.37' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='5.02' y1='14.17' x2='5.02' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">Total</th>
<td headers="grand_summary_stub_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 an2010" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">62,257</td>
<td headers="grand_summary_stub_1 an2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">79,639</td>
<td headers="grand_summary_stub_1 an2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">80,453</td>
<td headers="grand_summary_stub_1 diff_abs2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">17,382</td>
<td headers="grand_summary_stub_1 diff_abs2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">18,196</td>
<td headers="grand_summary_stub_1 diff_rel2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 diff_rel2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 DUPE_COLUMN_PLT" class="gt_row gt_left gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::



# profondeur 2    

Bon, c'est rendu ici que je me suis rendu compte que je ne peux pas juste garder "profondeur ==2" car le total ne balancerait  plus (total prodondeur 2 = 52 127 vs  vrai total de 62 257 en 2010). Pour compenser ça, à partir de la profondeur 2 je garde les ligne de profondeur 2 *ainsi que les lignes de profondeur <2 et qui n'ont pas d'"enfants"*.


::: {.cell .column-screen-inset}

````{.cell-code}
```{{r}}
#| column: screen-inset
tableau_wide %>%
  group_by(profondeur ) %>% 
  summarise(total = sum(an2010, na.rm = TRUE))
```
````

::: {.cell-output .cell-output-stdout}

```
# A tibble: 8 × 2
  profondeur total
       <int> <dbl>
1          0 62257
2          1 62257
3          2 52127
4          3 48755
5          4 45801
6          5 26542
7          6  6463
8          7   637
```


:::
:::



Bon voici le tableau.   

LE transport est plus bas en 2021 qu'en 2010 (-5 % duh confinement), mais il était déjà pas vraiment beaucoup plus haut en 2019 (+5%), ce que j'ai trouvé étonnant.     

Même chose pour les vêtements, ils ont absolument été dévastés en 2021 (-31% vs 2010 duh, remote work) , mais ils étaient déjà moins important en 2019 qu'en 2010 (-5%).  

Matériel de lecture aussi est amusant.  C'est un petit poste de dépenses ( 189$ en 2010), qui avait chûté en 2019 (138\$), mais qui a remonté en 2021 (178 \$).  Est-ce que c'est un boom de lecture de livres et de revues? Il me semble que j'en ai pas vraiment entendu parler.  

Le logement, très cher, on sait..


::: {.cell .column-screen-inset}

````{.cell-code}
```{{r}}
#| column: screen-inset
tableau_wide %>%
  filter(profondeur == 2 |( profondeur<2 & last_profondeur==TRUE) )%>%
  select(-profondeur, -last_profondeur) %>% 
  gt::gt() %>%
  gt::cols_label(.list= setNames(as.list(names_with_spaces),names(tableau_wide%>% select(-profondeur, -last_profondeur)) )) %>%  ###  this is clever af simon!! quick tip to replace all "_" with " " in the column labels
  fmt_number(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), decimals = 0) %>%
  fmt_percent(columns = c(diff_rel2019, diff_rel2021)) %>% 
  gt::grand_summary_rows(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), 
                         fns = list(Total ~ sum(.,na.rm = TRUE)) ,
                         fmt = ~fmt_number(., decimals = 0)) %>%
  gt_plt_bar(column = diff_rel2019, keep_column = TRUE, color = cerulean_blue ) %>% 
  gt::sub_missing(missing_text = "-")
```
````

::: {.cell-output-display}


```{=html}
<div id="vdqiummlye" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#vdqiummlye table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#vdqiummlye thead, #vdqiummlye tbody, #vdqiummlye tfoot, #vdqiummlye tr, #vdqiummlye td, #vdqiummlye th {
  border-style: none;
}

#vdqiummlye p {
  margin: 0;
  padding: 0;
}

#vdqiummlye .gt_table {
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

#vdqiummlye .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#vdqiummlye .gt_title {
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

#vdqiummlye .gt_subtitle {
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

#vdqiummlye .gt_heading {
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

#vdqiummlye .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vdqiummlye .gt_col_headings {
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

#vdqiummlye .gt_col_heading {
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

#vdqiummlye .gt_column_spanner_outer {
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

#vdqiummlye .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#vdqiummlye .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#vdqiummlye .gt_column_spanner {
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

#vdqiummlye .gt_spanner_row {
  border-bottom-style: hidden;
}

#vdqiummlye .gt_group_heading {
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

#vdqiummlye .gt_empty_group_heading {
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

#vdqiummlye .gt_from_md > :first-child {
  margin-top: 0;
}

#vdqiummlye .gt_from_md > :last-child {
  margin-bottom: 0;
}

#vdqiummlye .gt_row {
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

#vdqiummlye .gt_stub {
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

#vdqiummlye .gt_stub_row_group {
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

#vdqiummlye .gt_row_group_first td {
  border-top-width: 2px;
}

#vdqiummlye .gt_row_group_first th {
  border-top-width: 2px;
}

#vdqiummlye .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#vdqiummlye .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#vdqiummlye .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#vdqiummlye .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vdqiummlye .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#vdqiummlye .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#vdqiummlye .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#vdqiummlye .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#vdqiummlye .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vdqiummlye .gt_footnotes {
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

#vdqiummlye .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#vdqiummlye .gt_sourcenotes {
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

#vdqiummlye .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#vdqiummlye .gt_left {
  text-align: left;
}

#vdqiummlye .gt_center {
  text-align: center;
}

#vdqiummlye .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#vdqiummlye .gt_font_normal {
  font-weight: normal;
}

#vdqiummlye .gt_font_bold {
  font-weight: bold;
}

#vdqiummlye .gt_font_italic {
  font-style: italic;
}

#vdqiummlye .gt_super {
  font-size: 65%;
}

#vdqiummlye .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#vdqiummlye .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#vdqiummlye .gt_indent_1 {
  text-indent: 5px;
}

#vdqiummlye .gt_indent_2 {
  text-indent: 10px;
}

#vdqiummlye .gt_indent_3 {
  text-indent: 15px;
}

#vdqiummlye .gt_indent_4 {
  text-indent: 20px;
}

#vdqiummlye .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="hierarchie pour depenses des menages categories de niveau sommaire">hierarchie pour depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="depenses des menages categories de niveau sommaire">depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2010">an2010</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2019">an2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2021">an2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2019">diff abs2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2021">diff abs2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2019">diff rel2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2021">diff rel2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="diff_rel2019">diff_rel2019</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12</td>
<td headers="stub_1_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dépenses courantes</td>
<td headers="stub_1_1 an2010" class="gt_row gt_right">3,291</td>
<td headers="stub_1_1 an2019" class="gt_row gt_right">4,398</td>
<td headers="stub_1_1 an2021" class="gt_row gt_right">4,548</td>
<td headers="stub_1_1 diff_abs2019" class="gt_row gt_right">1,107</td>
<td headers="stub_1_1 diff_abs2021" class="gt_row gt_right">1,257</td>
<td headers="stub_1_1 diff_rel2019" class="gt_row gt_right">33.64%</td>
<td headers="stub_1_1 diff_rel2021" class="gt_row gt_right">38.20%</td>
<td headers="stub_1_1 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='26.48' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_2 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14</td>
<td headers="stub_1_2 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Ameublement et équipement ménagers</td>
<td headers="stub_1_2 an2010" class="gt_row gt_right">1,620</td>
<td headers="stub_1_2 an2019" class="gt_row gt_right">2,100</td>
<td headers="stub_1_2 an2021" class="gt_row gt_right">3,105</td>
<td headers="stub_1_2 diff_abs2019" class="gt_row gt_right">480</td>
<td headers="stub_1_2 diff_abs2021" class="gt_row gt_right">1,485</td>
<td headers="stub_1_2 diff_rel2019" class="gt_row gt_right">29.63%</td>
<td headers="stub_1_2 diff_rel2021" class="gt_row gt_right">91.67%</td>
<td headers="stub_1_2 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='23.33' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_3 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18</td>
<td headers="stub_1_3 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements et accessoires</td>
<td headers="stub_1_3 an2010" class="gt_row gt_right">3,173</td>
<td headers="stub_1_3 an2019" class="gt_row gt_right">3,014</td>
<td headers="stub_1_3 an2021" class="gt_row gt_right">2,183</td>
<td headers="stub_1_3 diff_abs2019" class="gt_row gt_right">−159</td>
<td headers="stub_1_3 diff_abs2021" class="gt_row gt_right">−990</td>
<td headers="stub_1_3 diff_rel2019" class="gt_row gt_right">−5.01%</td>
<td headers="stub_1_3 diff_rel2021" class="gt_row gt_right">−31.20%</td>
<td headers="stub_1_3 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='22.74' y='0.89' width='3.95' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_4 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23</td>
<td headers="stub_1_4 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Transport</td>
<td headers="stub_1_4 an2010" class="gt_row gt_right">9,987</td>
<td headers="stub_1_4 an2019" class="gt_row gt_right">10,492</td>
<td headers="stub_1_4 an2021" class="gt_row gt_right">9,409</td>
<td headers="stub_1_4 diff_abs2019" class="gt_row gt_right">505</td>
<td headers="stub_1_4 diff_abs2021" class="gt_row gt_right">−578</td>
<td headers="stub_1_4 diff_rel2019" class="gt_row gt_right">5.06%</td>
<td headers="stub_1_4 diff_rel2021" class="gt_row gt_right">−5.79%</td>
<td headers="stub_1_4 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='3.98' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_5" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_5 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26</td>
<td headers="stub_1_5 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Soins de santé</td>
<td headers="stub_1_5 an2010" class="gt_row gt_right">2,612</td>
<td headers="stub_1_5 an2019" class="gt_row gt_right">2,964</td>
<td headers="stub_1_5 an2021" class="gt_row gt_right">2,897</td>
<td headers="stub_1_5 diff_abs2019" class="gt_row gt_right">352</td>
<td headers="stub_1_5 diff_abs2021" class="gt_row gt_right">285</td>
<td headers="stub_1_5 diff_rel2019" class="gt_row gt_right">13.48%</td>
<td headers="stub_1_5 diff_rel2021" class="gt_row gt_right">10.91%</td>
<td headers="stub_1_5 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='10.61' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_6" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_6 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29</td>
<td headers="stub_1_6 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Soins personnels</td>
<td headers="stub_1_6 an2010" class="gt_row gt_right">998</td>
<td headers="stub_1_6 an2019" class="gt_row gt_right">1,236</td>
<td headers="stub_1_6 an2021" class="gt_row gt_right">1,444</td>
<td headers="stub_1_6 diff_abs2019" class="gt_row gt_right">238</td>
<td headers="stub_1_6 diff_abs2021" class="gt_row gt_right">446</td>
<td headers="stub_1_6 diff_rel2019" class="gt_row gt_right">23.85%</td>
<td headers="stub_1_6 diff_rel2021" class="gt_row gt_right">44.69%</td>
<td headers="stub_1_6 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='18.78' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_7" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_7 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3</td>
<td headers="stub_1_7 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dépenses alimentaires</td>
<td headers="stub_1_7 an2010" class="gt_row gt_right">7,409</td>
<td headers="stub_1_7 an2019" class="gt_row gt_right">9,847</td>
<td headers="stub_1_7 an2021" class="gt_row gt_right">9,731</td>
<td headers="stub_1_7 diff_abs2019" class="gt_row gt_right">2,438</td>
<td headers="stub_1_7 diff_abs2021" class="gt_row gt_right">2,322</td>
<td headers="stub_1_7 diff_rel2019" class="gt_row gt_right">32.91%</td>
<td headers="stub_1_7 diff_rel2021" class="gt_row gt_right">31.34%</td>
<td headers="stub_1_7 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='25.91' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_8" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_8 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30</td>
<td headers="stub_1_8 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Loisirs</td>
<td headers="stub_1_8 an2010" class="gt_row gt_right">3,184</td>
<td headers="stub_1_8 an2019" class="gt_row gt_right">3,776</td>
<td headers="stub_1_8 an2021" class="gt_row gt_right">3,803</td>
<td headers="stub_1_8 diff_abs2019" class="gt_row gt_right">592</td>
<td headers="stub_1_8 diff_abs2021" class="gt_row gt_right">619</td>
<td headers="stub_1_8 diff_rel2019" class="gt_row gt_right">18.59%</td>
<td headers="stub_1_8 diff_rel2021" class="gt_row gt_right">19.44%</td>
<td headers="stub_1_8 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='14.64' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_9" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_9 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35</td>
<td headers="stub_1_9 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Éducation</td>
<td headers="stub_1_9 an2010" class="gt_row gt_right">644</td>
<td headers="stub_1_9 an2019" class="gt_row gt_right">936</td>
<td headers="stub_1_9 an2021" class="gt_row gt_right">1,042</td>
<td headers="stub_1_9 diff_abs2019" class="gt_row gt_right">292</td>
<td headers="stub_1_9 diff_abs2021" class="gt_row gt_right">398</td>
<td headers="stub_1_9 diff_rel2019" class="gt_row gt_right">45.34%</td>
<td headers="stub_1_9 diff_rel2021" class="gt_row gt_right">61.80%</td>
<td headers="stub_1_9 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='35.70' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_10" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_10 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.359</td>
<td headers="stub_1_10 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits de tabac, boissons alcoolisées et cannabis pour usage non-thérapeutique</td>
<td headers="stub_1_10 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_10 an2019" class="gt_row gt_right">1,894</td>
<td headers="stub_1_10 an2021" class="gt_row gt_right">1,859</td>
<td headers="stub_1_10 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_10 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_10 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_10 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_10 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_11" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_11 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36</td>
<td headers="stub_1_11 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel de lecture et autres imprimés</td>
<td headers="stub_1_11 an2010" class="gt_row gt_right">189</td>
<td headers="stub_1_11 an2019" class="gt_row gt_right">138</td>
<td headers="stub_1_11 an2021" class="gt_row gt_right">178</td>
<td headers="stub_1_11 diff_abs2019" class="gt_row gt_right">−51</td>
<td headers="stub_1_11 diff_abs2021" class="gt_row gt_right">−11</td>
<td headers="stub_1_11 diff_rel2019" class="gt_row gt_right">−26.98%</td>
<td headers="stub_1_11 diff_rel2021" class="gt_row gt_right">−5.82%</td>
<td headers="stub_1_11 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.44' y='0.89' width='21.25' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_12" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_12 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37</td>
<td headers="stub_1_12 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits de tabac et boissons alcoolisées</td>
<td headers="stub_1_12 an2010" class="gt_row gt_right">1,417</td>
<td headers="stub_1_12 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_12 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_12 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_12 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_12 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_12 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_12 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_13" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_13 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.38</td>
<td headers="stub_1_13 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Jeux de hasard</td>
<td headers="stub_1_13 an2010" class="gt_row gt_right">153</td>
<td headers="stub_1_13 an2019" class="gt_row gt_right">173</td>
<td headers="stub_1_13 an2021" class="gt_row gt_right">163</td>
<td headers="stub_1_13 diff_abs2019" class="gt_row gt_right">20</td>
<td headers="stub_1_13 diff_abs2021" class="gt_row gt_right">10</td>
<td headers="stub_1_13 diff_rel2019" class="gt_row gt_right">13.07%</td>
<td headers="stub_1_13 diff_rel2021" class="gt_row gt_right">6.54%</td>
<td headers="stub_1_13 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='10.29' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_14" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_14 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39</td>
<td headers="stub_1_14 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dépenses diverses</td>
<td headers="stub_1_14 an2010" class="gt_row gt_right">1,053</td>
<td headers="stub_1_14 an2019" class="gt_row gt_right">1,421</td>
<td headers="stub_1_14 an2021" class="gt_row gt_right">1,644</td>
<td headers="stub_1_14 diff_abs2019" class="gt_row gt_right">368</td>
<td headers="stub_1_14 diff_abs2021" class="gt_row gt_right">591</td>
<td headers="stub_1_14 diff_rel2019" class="gt_row gt_right">34.95%</td>
<td headers="stub_1_14 diff_rel2021" class="gt_row gt_right">56.13%</td>
<td headers="stub_1_14 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='27.52' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_15" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_15 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6</td>
<td headers="stub_1_15 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Logement</td>
<td headers="stub_1_15 an2010" class="gt_row gt_right">12,022</td>
<td headers="stub_1_15 an2019" class="gt_row gt_right">15,821</td>
<td headers="stub_1_15 an2021" class="gt_row gt_right">15,882</td>
<td headers="stub_1_15 diff_abs2019" class="gt_row gt_right">3,799</td>
<td headers="stub_1_15 diff_abs2021" class="gt_row gt_right">3,860</td>
<td headers="stub_1_15 diff_rel2019" class="gt_row gt_right">31.60%</td>
<td headers="stub_1_15 diff_rel2021" class="gt_row gt_right">32.11%</td>
<td headers="stub_1_15 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='24.88' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_16" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_16 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.40</td>
<td headers="stub_1_16 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Impôts sur le revenu</td>
<td headers="stub_1_16 an2010" class="gt_row gt_right">10,130</td>
<td headers="stub_1_16 an2019" class="gt_row gt_right">15,030</td>
<td headers="stub_1_16 an2021" class="gt_row gt_right">16,342</td>
<td headers="stub_1_16 diff_abs2019" class="gt_row gt_right">4,900</td>
<td headers="stub_1_16 diff_abs2021" class="gt_row gt_right">6,212</td>
<td headers="stub_1_16 diff_rel2019" class="gt_row gt_right">48.37%</td>
<td headers="stub_1_16 diff_rel2021" class="gt_row gt_right">61.32%</td>
<td headers="stub_1_16 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='38.08' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_17" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_17 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.307</td>
<td headers="stub_1_17 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-emploi et d'assurance-parentale du Québec</td>
<td headers="stub_1_17 an2010" class="gt_row gt_right">417</td>
<td headers="stub_1_17 an2019" class="gt_row gt_right">756</td>
<td headers="stub_1_17 an2021" class="gt_row gt_right">709</td>
<td headers="stub_1_17 diff_abs2019" class="gt_row gt_right">339</td>
<td headers="stub_1_17 diff_abs2021" class="gt_row gt_right">292</td>
<td headers="stub_1_17 diff_rel2019" class="gt_row gt_right">81.29%</td>
<td headers="stub_1_17 diff_rel2021" class="gt_row gt_right">70.02%</td>
<td headers="stub_1_17 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='64.01' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_18" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_18 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.308</td>
<td headers="stub_1_18 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cotisations à des caisses de retraite ou de pension</td>
<td headers="stub_1_18 an2010" class="gt_row gt_right">2,529</td>
<td headers="stub_1_18 an2019" class="gt_row gt_right">3,775</td>
<td headers="stub_1_18 an2021" class="gt_row gt_right">4,126</td>
<td headers="stub_1_18 diff_abs2019" class="gt_row gt_right">1,246</td>
<td headers="stub_1_18 diff_abs2021" class="gt_row gt_right">1,597</td>
<td headers="stub_1_18 diff_rel2019" class="gt_row gt_right">49.27%</td>
<td headers="stub_1_18 diff_rel2021" class="gt_row gt_right">63.15%</td>
<td headers="stub_1_18 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='38.79' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_19" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_19 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.309</td>
<td headers="stub_1_19 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Contrats de rentes et argent transféré à des FERR</td>
<td headers="stub_1_19 an2010" class="gt_row gt_right">96</td>
<td headers="stub_1_19 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_19 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_19 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_19 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_19 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_19 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_19 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_20" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_20 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.310</td>
<td headers="stub_1_20 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-vie, d'assurances temporaires et d'assurances mixtes</td>
<td headers="stub_1_20 an2010" class="gt_row gt_right">587</td>
<td headers="stub_1_20 an2019" class="gt_row gt_right">656</td>
<td headers="stub_1_20 an2021" class="gt_row gt_right">587</td>
<td headers="stub_1_20 diff_abs2019" class="gt_row gt_right">69</td>
<td headers="stub_1_20 diff_abs2021" class="gt_row gt_right">0</td>
<td headers="stub_1_20 diff_rel2019" class="gt_row gt_right">11.75%</td>
<td headers="stub_1_20 diff_rel2021" class="gt_row gt_right">0.00%</td>
<td headers="stub_1_20 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='9.25' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_21" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_21 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311</td>
<td headers="stub_1_21 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux en argent et pensions alimentaires</td>
<td headers="stub_1_21 an2010" class="gt_row gt_right">491</td>
<td headers="stub_1_21 an2019" class="gt_row gt_right">972</td>
<td headers="stub_1_21 an2021" class="gt_row gt_right">579</td>
<td headers="stub_1_21 diff_abs2019" class="gt_row gt_right">481</td>
<td headers="stub_1_21 diff_abs2021" class="gt_row gt_right">88</td>
<td headers="stub_1_21 diff_rel2019" class="gt_row gt_right">97.96%</td>
<td headers="stub_1_21 diff_rel2021" class="gt_row gt_right">17.92%</td>
<td headers="stub_1_21 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='77.13' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_22" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_22 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.315</td>
<td headers="stub_1_22 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dons de bienfaisance</td>
<td headers="stub_1_22 an2010" class="gt_row gt_right">255</td>
<td headers="stub_1_22 an2019" class="gt_row gt_right">244</td>
<td headers="stub_1_22 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_22 diff_abs2019" class="gt_row gt_right">−11</td>
<td headers="stub_1_22 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_22 diff_rel2019" class="gt_row gt_right">−4.31%</td>
<td headers="stub_1_22 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_22 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='23.29' y='0.89' width='3.40' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_23" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_23 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.315</td>
<td headers="stub_1_23 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dons de bienfaisance</td>
<td headers="stub_1_23 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_23 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_23 an2021" class="gt_row gt_right">222</td>
<td headers="stub_1_23 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_23 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_23 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_23 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_23 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">Total</th>
<td headers="grand_summary_stub_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 an2010" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">62,257</td>
<td headers="grand_summary_stub_1 an2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">79,643</td>
<td headers="grand_summary_stub_1 an2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">80,453</td>
<td headers="grand_summary_stub_1 diff_abs2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">17,005</td>
<td headers="grand_summary_stub_1 diff_abs2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">17,883</td>
<td headers="grand_summary_stub_1 diff_rel2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 diff_rel2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 DUPE_COLUMN_PLT" class="gt_row gt_left gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::




voici aussi le top 5 "plus gross hausse" et "plus petit hausse pour la route.  


::: {.cell .column-screen-inset}

````{.cell-code}
```{{r}}
#| column: screen-inset

bind_rows(
  tableau_wide %>% 
    filter(!is.na(diff_rel2019) & (profondeur == 2 | (profondeur < 2 & last_profondeur==TRUE )))%>%
    arrange(diff_rel2019) %>%
    head(5),
  tableau_wide %>% 
    filter(!is.na(diff_rel2019) & (profondeur == 2 | (profondeur < 2 & last_profondeur==TRUE )))%>%
    arrange(diff_rel2019) %>%
    tail(5)
) %>% 
  select(-profondeur, -last_profondeur) %>% 
  gt::gt() %>%
  gt::cols_label(.list= setNames(as.list(names_with_spaces),names(tableau_wide%>% select(-profondeur, -last_profondeur)) )) %>%  ###  this is clever af simon!! quick tip to replace all "_" with " " in the column labels
  fmt_number(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), decimals = 0) %>%
  fmt_percent(columns = c(diff_rel2019, diff_rel2021)) %>% 
  gt::grand_summary_rows(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), 
                         fns = list(Total ~ sum(.,na.rm = TRUE)) ,
                         fmt = ~fmt_number(., decimals = 0)) %>%
  gt_plt_bar(column = diff_rel2019, keep_column = TRUE, color = cerulean_blue ) %>% 
  gt::sub_missing(missing_text = "-")
```
````

::: {.cell-output-display}


```{=html}
<div id="vobipngfhf" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#vobipngfhf table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#vobipngfhf thead, #vobipngfhf tbody, #vobipngfhf tfoot, #vobipngfhf tr, #vobipngfhf td, #vobipngfhf th {
  border-style: none;
}

#vobipngfhf p {
  margin: 0;
  padding: 0;
}

#vobipngfhf .gt_table {
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

#vobipngfhf .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#vobipngfhf .gt_title {
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

#vobipngfhf .gt_subtitle {
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

#vobipngfhf .gt_heading {
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

#vobipngfhf .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vobipngfhf .gt_col_headings {
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

#vobipngfhf .gt_col_heading {
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

#vobipngfhf .gt_column_spanner_outer {
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

#vobipngfhf .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#vobipngfhf .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#vobipngfhf .gt_column_spanner {
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

#vobipngfhf .gt_spanner_row {
  border-bottom-style: hidden;
}

#vobipngfhf .gt_group_heading {
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

#vobipngfhf .gt_empty_group_heading {
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

#vobipngfhf .gt_from_md > :first-child {
  margin-top: 0;
}

#vobipngfhf .gt_from_md > :last-child {
  margin-bottom: 0;
}

#vobipngfhf .gt_row {
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

#vobipngfhf .gt_stub {
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

#vobipngfhf .gt_stub_row_group {
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

#vobipngfhf .gt_row_group_first td {
  border-top-width: 2px;
}

#vobipngfhf .gt_row_group_first th {
  border-top-width: 2px;
}

#vobipngfhf .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#vobipngfhf .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#vobipngfhf .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#vobipngfhf .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vobipngfhf .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#vobipngfhf .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#vobipngfhf .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#vobipngfhf .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#vobipngfhf .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vobipngfhf .gt_footnotes {
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

#vobipngfhf .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#vobipngfhf .gt_sourcenotes {
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

#vobipngfhf .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#vobipngfhf .gt_left {
  text-align: left;
}

#vobipngfhf .gt_center {
  text-align: center;
}

#vobipngfhf .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#vobipngfhf .gt_font_normal {
  font-weight: normal;
}

#vobipngfhf .gt_font_bold {
  font-weight: bold;
}

#vobipngfhf .gt_font_italic {
  font-style: italic;
}

#vobipngfhf .gt_super {
  font-size: 65%;
}

#vobipngfhf .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#vobipngfhf .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#vobipngfhf .gt_indent_1 {
  text-indent: 5px;
}

#vobipngfhf .gt_indent_2 {
  text-indent: 10px;
}

#vobipngfhf .gt_indent_3 {
  text-indent: 15px;
}

#vobipngfhf .gt_indent_4 {
  text-indent: 20px;
}

#vobipngfhf .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="hierarchie pour depenses des menages categories de niveau sommaire">hierarchie pour depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="depenses des menages categories de niveau sommaire">depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2010">an2010</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2019">an2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2021">an2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2019">diff abs2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2021">diff abs2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2019">diff rel2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2021">diff rel2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="diff_rel2019">diff_rel2019</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36</td>
<td headers="stub_1_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel de lecture et autres imprimés</td>
<td headers="stub_1_1 an2010" class="gt_row gt_right">189</td>
<td headers="stub_1_1 an2019" class="gt_row gt_right">138</td>
<td headers="stub_1_1 an2021" class="gt_row gt_right">178</td>
<td headers="stub_1_1 diff_abs2019" class="gt_row gt_right">−51</td>
<td headers="stub_1_1 diff_abs2021" class="gt_row gt_right">−11</td>
<td headers="stub_1_1 diff_rel2019" class="gt_row gt_right">−26.98%</td>
<td headers="stub_1_1 diff_rel2021" class="gt_row gt_right">−5.82%</td>
<td headers="stub_1_1 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.44' y='0.89' width='21.25' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_2 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18</td>
<td headers="stub_1_2 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements et accessoires</td>
<td headers="stub_1_2 an2010" class="gt_row gt_right">3,173</td>
<td headers="stub_1_2 an2019" class="gt_row gt_right">3,014</td>
<td headers="stub_1_2 an2021" class="gt_row gt_right">2,183</td>
<td headers="stub_1_2 diff_abs2019" class="gt_row gt_right">−159</td>
<td headers="stub_1_2 diff_abs2021" class="gt_row gt_right">−990</td>
<td headers="stub_1_2 diff_rel2019" class="gt_row gt_right">−5.01%</td>
<td headers="stub_1_2 diff_rel2021" class="gt_row gt_right">−31.20%</td>
<td headers="stub_1_2 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='22.74' y='0.89' width='3.95' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_3 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.315</td>
<td headers="stub_1_3 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dons de bienfaisance</td>
<td headers="stub_1_3 an2010" class="gt_row gt_right">255</td>
<td headers="stub_1_3 an2019" class="gt_row gt_right">244</td>
<td headers="stub_1_3 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_3 diff_abs2019" class="gt_row gt_right">−11</td>
<td headers="stub_1_3 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_3 diff_rel2019" class="gt_row gt_right">−4.31%</td>
<td headers="stub_1_3 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_3 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='23.29' y='0.89' width='3.40' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_4 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23</td>
<td headers="stub_1_4 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Transport</td>
<td headers="stub_1_4 an2010" class="gt_row gt_right">9,987</td>
<td headers="stub_1_4 an2019" class="gt_row gt_right">10,492</td>
<td headers="stub_1_4 an2021" class="gt_row gt_right">9,409</td>
<td headers="stub_1_4 diff_abs2019" class="gt_row gt_right">505</td>
<td headers="stub_1_4 diff_abs2021" class="gt_row gt_right">−578</td>
<td headers="stub_1_4 diff_rel2019" class="gt_row gt_right">5.06%</td>
<td headers="stub_1_4 diff_rel2021" class="gt_row gt_right">−5.79%</td>
<td headers="stub_1_4 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='3.98' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_5" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_5 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.310</td>
<td headers="stub_1_5 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-vie, d'assurances temporaires et d'assurances mixtes</td>
<td headers="stub_1_5 an2010" class="gt_row gt_right">587</td>
<td headers="stub_1_5 an2019" class="gt_row gt_right">656</td>
<td headers="stub_1_5 an2021" class="gt_row gt_right">587</td>
<td headers="stub_1_5 diff_abs2019" class="gt_row gt_right">69</td>
<td headers="stub_1_5 diff_abs2021" class="gt_row gt_right">0</td>
<td headers="stub_1_5 diff_rel2019" class="gt_row gt_right">11.75%</td>
<td headers="stub_1_5 diff_rel2021" class="gt_row gt_right">0.00%</td>
<td headers="stub_1_5 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='9.25' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_6" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_6 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35</td>
<td headers="stub_1_6 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Éducation</td>
<td headers="stub_1_6 an2010" class="gt_row gt_right">644</td>
<td headers="stub_1_6 an2019" class="gt_row gt_right">936</td>
<td headers="stub_1_6 an2021" class="gt_row gt_right">1,042</td>
<td headers="stub_1_6 diff_abs2019" class="gt_row gt_right">292</td>
<td headers="stub_1_6 diff_abs2021" class="gt_row gt_right">398</td>
<td headers="stub_1_6 diff_rel2019" class="gt_row gt_right">45.34%</td>
<td headers="stub_1_6 diff_rel2021" class="gt_row gt_right">61.80%</td>
<td headers="stub_1_6 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='35.70' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_7" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_7 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.40</td>
<td headers="stub_1_7 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Impôts sur le revenu</td>
<td headers="stub_1_7 an2010" class="gt_row gt_right">10,130</td>
<td headers="stub_1_7 an2019" class="gt_row gt_right">15,030</td>
<td headers="stub_1_7 an2021" class="gt_row gt_right">16,342</td>
<td headers="stub_1_7 diff_abs2019" class="gt_row gt_right">4,900</td>
<td headers="stub_1_7 diff_abs2021" class="gt_row gt_right">6,212</td>
<td headers="stub_1_7 diff_rel2019" class="gt_row gt_right">48.37%</td>
<td headers="stub_1_7 diff_rel2021" class="gt_row gt_right">61.32%</td>
<td headers="stub_1_7 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='38.08' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_8" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_8 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.308</td>
<td headers="stub_1_8 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cotisations à des caisses de retraite ou de pension</td>
<td headers="stub_1_8 an2010" class="gt_row gt_right">2,529</td>
<td headers="stub_1_8 an2019" class="gt_row gt_right">3,775</td>
<td headers="stub_1_8 an2021" class="gt_row gt_right">4,126</td>
<td headers="stub_1_8 diff_abs2019" class="gt_row gt_right">1,246</td>
<td headers="stub_1_8 diff_abs2021" class="gt_row gt_right">1,597</td>
<td headers="stub_1_8 diff_rel2019" class="gt_row gt_right">49.27%</td>
<td headers="stub_1_8 diff_rel2021" class="gt_row gt_right">63.15%</td>
<td headers="stub_1_8 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='38.79' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_9" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_9 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.307</td>
<td headers="stub_1_9 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-emploi et d'assurance-parentale du Québec</td>
<td headers="stub_1_9 an2010" class="gt_row gt_right">417</td>
<td headers="stub_1_9 an2019" class="gt_row gt_right">756</td>
<td headers="stub_1_9 an2021" class="gt_row gt_right">709</td>
<td headers="stub_1_9 diff_abs2019" class="gt_row gt_right">339</td>
<td headers="stub_1_9 diff_abs2021" class="gt_row gt_right">292</td>
<td headers="stub_1_9 diff_rel2019" class="gt_row gt_right">81.29%</td>
<td headers="stub_1_9 diff_rel2021" class="gt_row gt_right">70.02%</td>
<td headers="stub_1_9 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='64.01' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_10" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_10 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311</td>
<td headers="stub_1_10 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux en argent et pensions alimentaires</td>
<td headers="stub_1_10 an2010" class="gt_row gt_right">491</td>
<td headers="stub_1_10 an2019" class="gt_row gt_right">972</td>
<td headers="stub_1_10 an2021" class="gt_row gt_right">579</td>
<td headers="stub_1_10 diff_abs2019" class="gt_row gt_right">481</td>
<td headers="stub_1_10 diff_abs2021" class="gt_row gt_right">88</td>
<td headers="stub_1_10 diff_rel2019" class="gt_row gt_right">97.96%</td>
<td headers="stub_1_10 diff_rel2021" class="gt_row gt_right">17.92%</td>
<td headers="stub_1_10 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.69' y='0.89' width='77.13' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='26.69' y1='14.17' x2='26.69' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">Total</th>
<td headers="grand_summary_stub_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 an2010" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">28,402</td>
<td headers="grand_summary_stub_1 an2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">36,013</td>
<td headers="grand_summary_stub_1 an2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">35,155</td>
<td headers="grand_summary_stub_1 diff_abs2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">7,611</td>
<td headers="grand_summary_stub_1 diff_abs2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">7,008</td>
<td headers="grand_summary_stub_1 diff_rel2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 diff_rel2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 DUPE_COLUMN_PLT" class="gt_row gt_left gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::


# profondeur 3    

Bon là je vais me coucher, mais regardez bien transport.   Globalement c'est genre -5%, mais le transport public est à -40%.  yé covid  

::: {.cell .column-screen-inset}

````{.cell-code}
```{{r}}
#| column: screen-inset
tableau_wide %>% 
  filter(profondeur == 3 | (profondeur < 3 & last_profondeur==TRUE ))%>%
  select(-profondeur, -last_profondeur) %>% 
  gt::gt() %>%
  gt::cols_label(.list= setNames(as.list(names_with_spaces),names(tableau_wide%>% select(-profondeur, -last_profondeur)) )) %>%  ###  this is clever af simon!! quick tip to replace all "_" with " " in the column labels
  fmt_number(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), decimals = 0) %>%
  fmt_percent(columns = c(diff_rel2019, diff_rel2021)) %>% 
  gt::grand_summary_rows(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), 
                         fns = list(Total ~ sum(.,na.rm = TRUE)) ,
                         fmt = ~fmt_number(., decimals = 0)) %>%
  gt_plt_bar(column = diff_rel2019, keep_column = TRUE, color = cerulean_blue ) %>% 
  gt::sub_missing(missing_text = "-")
```
````

::: {.cell-output-display}


```{=html}
<div id="zjturxggac" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#zjturxggac table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#zjturxggac thead, #zjturxggac tbody, #zjturxggac tfoot, #zjturxggac tr, #zjturxggac td, #zjturxggac th {
  border-style: none;
}

#zjturxggac p {
  margin: 0;
  padding: 0;
}

#zjturxggac .gt_table {
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

#zjturxggac .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#zjturxggac .gt_title {
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

#zjturxggac .gt_subtitle {
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

#zjturxggac .gt_heading {
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

#zjturxggac .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#zjturxggac .gt_col_headings {
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

#zjturxggac .gt_col_heading {
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

#zjturxggac .gt_column_spanner_outer {
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

#zjturxggac .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#zjturxggac .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#zjturxggac .gt_column_spanner {
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

#zjturxggac .gt_spanner_row {
  border-bottom-style: hidden;
}

#zjturxggac .gt_group_heading {
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

#zjturxggac .gt_empty_group_heading {
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

#zjturxggac .gt_from_md > :first-child {
  margin-top: 0;
}

#zjturxggac .gt_from_md > :last-child {
  margin-bottom: 0;
}

#zjturxggac .gt_row {
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

#zjturxggac .gt_stub {
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

#zjturxggac .gt_stub_row_group {
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

#zjturxggac .gt_row_group_first td {
  border-top-width: 2px;
}

#zjturxggac .gt_row_group_first th {
  border-top-width: 2px;
}

#zjturxggac .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#zjturxggac .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#zjturxggac .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#zjturxggac .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#zjturxggac .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#zjturxggac .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#zjturxggac .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#zjturxggac .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#zjturxggac .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#zjturxggac .gt_footnotes {
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

#zjturxggac .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#zjturxggac .gt_sourcenotes {
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

#zjturxggac .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#zjturxggac .gt_left {
  text-align: left;
}

#zjturxggac .gt_center {
  text-align: center;
}

#zjturxggac .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#zjturxggac .gt_font_normal {
  font-weight: normal;
}

#zjturxggac .gt_font_bold {
  font-weight: bold;
}

#zjturxggac .gt_font_italic {
  font-style: italic;
}

#zjturxggac .gt_super {
  font-size: 65%;
}

#zjturxggac .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#zjturxggac .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#zjturxggac .gt_indent_1 {
  text-indent: 5px;
}

#zjturxggac .gt_indent_2 {
  text-indent: 10px;
}

#zjturxggac .gt_indent_3 {
  text-indent: 15px;
}

#zjturxggac .gt_indent_4 {
  text-indent: 20px;
}

#zjturxggac .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="hierarchie pour depenses des menages categories de niveau sommaire">hierarchie pour depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="depenses des menages categories de niveau sommaire">depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2010">an2010</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2019">an2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2021">an2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2019">diff abs2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2021">diff abs2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2019">diff rel2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2021">diff rel2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="diff_rel2019">diff_rel2019</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.103</td>
<td headers="stub_1_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Fournitures de jardinage et autres services</td>
<td headers="stub_1_1 an2010" class="gt_row gt_right">228</td>
<td headers="stub_1_1 an2019" class="gt_row gt_right">417</td>
<td headers="stub_1_1 an2021" class="gt_row gt_right">404</td>
<td headers="stub_1_1 diff_abs2019" class="gt_row gt_right">189</td>
<td headers="stub_1_1 diff_abs2021" class="gt_row gt_right">176</td>
<td headers="stub_1_1 diff_rel2019" class="gt_row gt_right">82.89%</td>
<td headers="stub_1_1 diff_rel2021" class="gt_row gt_right">77.19%</td>
<td headers="stub_1_1 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='25.61' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_2 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.107</td>
<td headers="stub_1_2 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres accessoires pour la maison</td>
<td headers="stub_1_2 an2010" class="gt_row gt_right">95</td>
<td headers="stub_1_2 an2019" class="gt_row gt_right">134</td>
<td headers="stub_1_2 an2021" class="gt_row gt_right">153</td>
<td headers="stub_1_2 diff_abs2019" class="gt_row gt_right">39</td>
<td headers="stub_1_2 diff_abs2021" class="gt_row gt_right">58</td>
<td headers="stub_1_2 diff_rel2019" class="gt_row gt_right">41.05%</td>
<td headers="stub_1_2 diff_rel2021" class="gt_row gt_right">61.05%</td>
<td headers="stub_1_2 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='12.68' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_3 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.108</td>
<td headers="stub_1_3 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Garde d'enfants</td>
<td headers="stub_1_3 an2010" class="gt_row gt_right">424</td>
<td headers="stub_1_3 an2019" class="gt_row gt_right">604</td>
<td headers="stub_1_3 an2021" class="gt_row gt_right">286</td>
<td headers="stub_1_3 diff_abs2019" class="gt_row gt_right">180</td>
<td headers="stub_1_3 diff_abs2021" class="gt_row gt_right">−138</td>
<td headers="stub_1_3 diff_rel2019" class="gt_row gt_right">42.45%</td>
<td headers="stub_1_3 diff_rel2021" class="gt_row gt_right">−32.55%</td>
<td headers="stub_1_3 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='13.12' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_4 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.13</td>
<td headers="stub_1_4 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Communications</td>
<td headers="stub_1_4 an2010" class="gt_row gt_right">1,367</td>
<td headers="stub_1_4 an2019" class="gt_row gt_right">2,075</td>
<td headers="stub_1_4 an2021" class="gt_row gt_right">2,342</td>
<td headers="stub_1_4 diff_abs2019" class="gt_row gt_right">708</td>
<td headers="stub_1_4 diff_abs2021" class="gt_row gt_right">975</td>
<td headers="stub_1_4 diff_rel2019" class="gt_row gt_right">51.79%</td>
<td headers="stub_1_4 diff_rel2021" class="gt_row gt_right">71.32%</td>
<td headers="stub_1_4 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='16.00' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_5" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_5 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.90</td>
<td headers="stub_1_5 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Aide domestique et autres services d'entretien ménager (sauf les services de garde)</td>
<td headers="stub_1_5 an2010" class="gt_row gt_right">236</td>
<td headers="stub_1_5 an2019" class="gt_row gt_right">157</td>
<td headers="stub_1_5 an2021" class="gt_row gt_right">155</td>
<td headers="stub_1_5 diff_abs2019" class="gt_row gt_right">−79</td>
<td headers="stub_1_5 diff_abs2021" class="gt_row gt_right">−81</td>
<td headers="stub_1_5 diff_rel2019" class="gt_row gt_right">−33.47%</td>
<td headers="stub_1_5 diff_rel2021" class="gt_row gt_right">−34.32%</td>
<td headers="stub_1_5 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='18.86' y='0.89' width='10.34' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_6" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_6 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.91</td>
<td headers="stub_1_6 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dépenses pour les animaux domestiques</td>
<td headers="stub_1_6 an2010" class="gt_row gt_right">384</td>
<td headers="stub_1_6 an2019" class="gt_row gt_right">452</td>
<td headers="stub_1_6 an2021" class="gt_row gt_right">519</td>
<td headers="stub_1_6 diff_abs2019" class="gt_row gt_right">68</td>
<td headers="stub_1_6 diff_abs2021" class="gt_row gt_right">135</td>
<td headers="stub_1_6 diff_rel2019" class="gt_row gt_right">17.71%</td>
<td headers="stub_1_6 diff_rel2021" class="gt_row gt_right">35.16%</td>
<td headers="stub_1_6 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='5.47' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_7" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_7 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.95</td>
<td headers="stub_1_7 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits et équipement de nettoyage</td>
<td headers="stub_1_7 an2010" class="gt_row gt_right">239</td>
<td headers="stub_1_7 an2019" class="gt_row gt_right">224</td>
<td headers="stub_1_7 an2021" class="gt_row gt_right">293</td>
<td headers="stub_1_7 diff_abs2019" class="gt_row gt_right">−15</td>
<td headers="stub_1_7 diff_abs2021" class="gt_row gt_right">54</td>
<td headers="stub_1_7 diff_rel2019" class="gt_row gt_right">−6.28%</td>
<td headers="stub_1_7 diff_rel2021" class="gt_row gt_right">22.59%</td>
<td headers="stub_1_7 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='27.26' y='0.89' width='1.94' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_8" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_8 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.99</td>
<td headers="stub_1_8 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Articles en papier, en plastique et en aluminium</td>
<td headers="stub_1_8 an2010" class="gt_row gt_right">319</td>
<td headers="stub_1_8 an2019" class="gt_row gt_right">335</td>
<td headers="stub_1_8 an2021" class="gt_row gt_right">396</td>
<td headers="stub_1_8 diff_abs2019" class="gt_row gt_right">16</td>
<td headers="stub_1_8 diff_abs2021" class="gt_row gt_right">77</td>
<td headers="stub_1_8 diff_rel2019" class="gt_row gt_right">5.02%</td>
<td headers="stub_1_8 diff_rel2021" class="gt_row gt_right">24.14%</td>
<td headers="stub_1_8 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='1.55' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_9" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_9 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.128</td>
<td headers="stub_1_9 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Entretien, location, réparations et services reliés à l'ameublement et à l'équipement ménager</td>
<td headers="stub_1_9 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_9 an2019" class="gt_row gt_right">41</td>
<td headers="stub_1_9 an2021" class="gt_row gt_right">117</td>
<td headers="stub_1_9 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_9 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_9 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_9 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_9 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_10" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_10 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.129</td>
<td headers="stub_1_10 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services reliés à l'ameublement et à l'équipement ménager</td>
<td headers="stub_1_10 an2010" class="gt_row gt_right">39</td>
<td headers="stub_1_10 an2019" class="gt_row gt_right">45</td>
<td headers="stub_1_10 an2021" class="gt_row gt_right">53</td>
<td headers="stub_1_10 diff_abs2019" class="gt_row gt_right">6</td>
<td headers="stub_1_10 diff_abs2021" class="gt_row gt_right">14</td>
<td headers="stub_1_10 diff_rel2019" class="gt_row gt_right">15.38%</td>
<td headers="stub_1_10 diff_rel2021" class="gt_row gt_right">35.90%</td>
<td headers="stub_1_10 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='4.75' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_11" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_11 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.15</td>
<td headers="stub_1_11 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Ameublement ménager</td>
<td headers="stub_1_11 an2010" class="gt_row gt_right">715</td>
<td headers="stub_1_11 an2019" class="gt_row gt_right">881</td>
<td headers="stub_1_11 an2021" class="gt_row gt_right">1,374</td>
<td headers="stub_1_11 diff_abs2019" class="gt_row gt_right">166</td>
<td headers="stub_1_11 diff_abs2021" class="gt_row gt_right">659</td>
<td headers="stub_1_11 diff_rel2019" class="gt_row gt_right">23.22%</td>
<td headers="stub_1_11 diff_rel2021" class="gt_row gt_right">92.17%</td>
<td headers="stub_1_11 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='7.17' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_12" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_12 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.16</td>
<td headers="stub_1_12 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Équipement ménager</td>
<td headers="stub_1_12 an2010" class="gt_row gt_right">836</td>
<td headers="stub_1_12 an2019" class="gt_row gt_right">1,133</td>
<td headers="stub_1_12 an2021" class="gt_row gt_right">1,561</td>
<td headers="stub_1_12 diff_abs2019" class="gt_row gt_right">297</td>
<td headers="stub_1_12 diff_abs2021" class="gt_row gt_right">725</td>
<td headers="stub_1_12 diff_rel2019" class="gt_row gt_right">35.53%</td>
<td headers="stub_1_12 diff_rel2021" class="gt_row gt_right">86.72%</td>
<td headers="stub_1_12 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='10.98' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_13" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_13 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.132</td>
<td headers="stub_1_13 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour femmes et filles (femmes et filles âgées de 4 ans et plus)</td>
<td headers="stub_1_13 an2010" class="gt_row gt_right">1,705</td>
<td headers="stub_1_13 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_13 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_13 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_13 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_13 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_13 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_13 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_14" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_14 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.141</td>
<td headers="stub_1_14 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour hommes et garçons (hommes et garçons âgés de 4 ans et plus)</td>
<td headers="stub_1_14 an2010" class="gt_row gt_right">1,050</td>
<td headers="stub_1_14 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_14 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_14 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_14 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_14 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_14 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_14 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_15" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_15 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.150</td>
<td headers="stub_1_15 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour enfants (enfants âgés de moins de 4 ans)</td>
<td headers="stub_1_15 an2010" class="gt_row gt_right">79</td>
<td headers="stub_1_15 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_15 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_15 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_15 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_15 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_15 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_15 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_16" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_16 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.153</td>
<td headers="stub_1_16 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux de vêtements à des personnes autres que les membres du ménage</td>
<td headers="stub_1_16 an2010" class="gt_row gt_right">290</td>
<td headers="stub_1_16 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_16 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_16 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_16 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_16 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_16 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_16 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_17" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_17 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.154</td>
<td headers="stub_1_17 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Tissus pour vêtements, fil à tricoter, fil et autres articles de couture</td>
<td headers="stub_1_17 an2010" class="gt_row gt_right">12</td>
<td headers="stub_1_17 an2019" class="gt_row gt_right">31</td>
<td headers="stub_1_17 an2021" class="gt_row gt_right">59</td>
<td headers="stub_1_17 diff_abs2019" class="gt_row gt_right">19</td>
<td headers="stub_1_17 diff_abs2021" class="gt_row gt_right">47</td>
<td headers="stub_1_17 diff_rel2019" class="gt_row gt_right">158.33%</td>
<td headers="stub_1_17 diff_rel2021" class="gt_row gt_right">391.67%</td>
<td headers="stub_1_17 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='48.92' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_18" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_18 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.155</td>
<td headers="stub_1_18 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services vestimentaires</td>
<td headers="stub_1_18 an2010" class="gt_row gt_right">36</td>
<td headers="stub_1_18 an2019" class="gt_row gt_right">123</td>
<td headers="stub_1_18 an2021" class="gt_row gt_right">90</td>
<td headers="stub_1_18 diff_abs2019" class="gt_row gt_right">87</td>
<td headers="stub_1_18 diff_abs2021" class="gt_row gt_right">54</td>
<td headers="stub_1_18 diff_rel2019" class="gt_row gt_right">241.67%</td>
<td headers="stub_1_18 diff_rel2021" class="gt_row gt_right">150.00%</td>
<td headers="stub_1_18 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='74.66' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_19" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_19 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.328</td>
<td headers="stub_1_19 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour femmes et filles (femmes et filles âgées de 14 ans et plus)</td>
<td headers="stub_1_19 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_19 an2019" class="gt_row gt_right">1,242</td>
<td headers="stub_1_19 an2021" class="gt_row gt_right">830</td>
<td headers="stub_1_19 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_19 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_19 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_19 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_19 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_20" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_20 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.331</td>
<td headers="stub_1_20 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour hommes et garçons (hommes et garçons âgés de 14 ans et plus)</td>
<td headers="stub_1_20 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_20 an2019" class="gt_row gt_right">833</td>
<td headers="stub_1_20 an2021" class="gt_row gt_right">541</td>
<td headers="stub_1_20 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_20 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_20 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_20 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_20 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_21" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_21 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.334</td>
<td headers="stub_1_21 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour enfants (enfants âgés de moins de 14 ans)</td>
<td headers="stub_1_21 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_21 an2019" class="gt_row gt_right">379</td>
<td headers="stub_1_21 an2021" class="gt_row gt_right">291</td>
<td headers="stub_1_21 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_21 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_21 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_21 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_21 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_22" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_22 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.337</td>
<td headers="stub_1_22 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Chaussures de sport</td>
<td headers="stub_1_22 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_22 an2019" class="gt_row gt_right">140</td>
<td headers="stub_1_22 an2021" class="gt_row gt_right">146</td>
<td headers="stub_1_22 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_22 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_22 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_22 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_22 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_23" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_23 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.338</td>
<td headers="stub_1_23 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Accessoires</td>
<td headers="stub_1_23 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_23 an2019" class="gt_row gt_right">139</td>
<td headers="stub_1_23 an2021" class="gt_row gt_right">130</td>
<td headers="stub_1_23 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_23 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_23 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_23 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_23 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_24" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_24 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.339</td>
<td headers="stub_1_24 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Montres et bijoux</td>
<td headers="stub_1_24 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_24 an2019" class="gt_row gt_right">127</td>
<td headers="stub_1_24 an2021" class="gt_row gt_right">97</td>
<td headers="stub_1_24 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_24 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_24 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_24 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_24 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_25" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_25 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.24</td>
<td headers="stub_1_25 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Transport privé</td>
<td headers="stub_1_25 an2010" class="gt_row gt_right">9,274</td>
<td headers="stub_1_25 an2019" class="gt_row gt_right">9,510</td>
<td headers="stub_1_25 an2021" class="gt_row gt_right">8,979</td>
<td headers="stub_1_25 diff_abs2019" class="gt_row gt_right">236</td>
<td headers="stub_1_25 diff_abs2021" class="gt_row gt_right">−295</td>
<td headers="stub_1_25 diff_rel2019" class="gt_row gt_right">2.54%</td>
<td headers="stub_1_25 diff_rel2021" class="gt_row gt_right">−3.18%</td>
<td headers="stub_1_25 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='0.79' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_26" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_26 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25</td>
<td headers="stub_1_26 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Transport public</td>
<td headers="stub_1_26 an2010" class="gt_row gt_right">713</td>
<td headers="stub_1_26 an2019" class="gt_row gt_right">982</td>
<td headers="stub_1_26 an2021" class="gt_row gt_right">429</td>
<td headers="stub_1_26 diff_abs2019" class="gt_row gt_right">269</td>
<td headers="stub_1_26 diff_abs2021" class="gt_row gt_right">−284</td>
<td headers="stub_1_26 diff_rel2019" class="gt_row gt_right">37.73%</td>
<td headers="stub_1_26 diff_rel2021" class="gt_row gt_right">−39.83%</td>
<td headers="stub_1_26 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='11.66' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_27" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_27 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.203</td>
<td headers="stub_1_27 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes pour les régimes privés d'assurance-maladie</td>
<td headers="stub_1_27 an2010" class="gt_row gt_right">613</td>
<td headers="stub_1_27 an2019" class="gt_row gt_right">1,144</td>
<td headers="stub_1_27 an2021" class="gt_row gt_right">839</td>
<td headers="stub_1_27 diff_abs2019" class="gt_row gt_right">531</td>
<td headers="stub_1_27 diff_abs2021" class="gt_row gt_right">226</td>
<td headers="stub_1_27 diff_rel2019" class="gt_row gt_right">86.62%</td>
<td headers="stub_1_27 diff_rel2021" class="gt_row gt_right">36.87%</td>
<td headers="stub_1_27 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='26.76' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_28" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_28 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.27</td>
<td headers="stub_1_28 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais directs de soins de santé défrayés par le ménage</td>
<td headers="stub_1_28 an2010" class="gt_row gt_right">1,707</td>
<td headers="stub_1_28 an2019" class="gt_row gt_right">1,819</td>
<td headers="stub_1_28 an2021" class="gt_row gt_right">2,058</td>
<td headers="stub_1_28 diff_abs2019" class="gt_row gt_right">112</td>
<td headers="stub_1_28 diff_abs2021" class="gt_row gt_right">351</td>
<td headers="stub_1_28 diff_rel2019" class="gt_row gt_right">6.56%</td>
<td headers="stub_1_28 diff_rel2021" class="gt_row gt_right">20.56%</td>
<td headers="stub_1_28 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='2.03' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_29" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_29 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.28</td>
<td headers="stub_1_29 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-maladie</td>
<td headers="stub_1_29 an2010" class="gt_row gt_right">905</td>
<td headers="stub_1_29 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_29 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_29 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_29 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_29 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_29 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_29 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_30" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_30 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.207</td>
<td headers="stub_1_30 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits de soins personnels</td>
<td headers="stub_1_30 an2010" class="gt_row gt_right">662</td>
<td headers="stub_1_30 an2019" class="gt_row gt_right">667</td>
<td headers="stub_1_30 an2021" class="gt_row gt_right">662</td>
<td headers="stub_1_30 diff_abs2019" class="gt_row gt_right">5</td>
<td headers="stub_1_30 diff_abs2021" class="gt_row gt_right">0</td>
<td headers="stub_1_30 diff_rel2019" class="gt_row gt_right">0.76%</td>
<td headers="stub_1_30 diff_rel2021" class="gt_row gt_right">0.00%</td>
<td headers="stub_1_30 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='0.23' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_31" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_31 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.217</td>
<td headers="stub_1_31 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de soins personnels</td>
<td headers="stub_1_31 an2010" class="gt_row gt_right">336</td>
<td headers="stub_1_31 an2019" class="gt_row gt_right">568</td>
<td headers="stub_1_31 an2021" class="gt_row gt_right">782</td>
<td headers="stub_1_31 diff_abs2019" class="gt_row gt_right">232</td>
<td headers="stub_1_31 diff_abs2021" class="gt_row gt_right">446</td>
<td headers="stub_1_31 diff_rel2019" class="gt_row gt_right">69.05%</td>
<td headers="stub_1_31 diff_rel2021" class="gt_row gt_right">132.74%</td>
<td headers="stub_1_31 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='21.33' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_32" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_32 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.364</td>
<td headers="stub_1_32 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de livraison de repas prêts-à-cuisiner</td>
<td headers="stub_1_32 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_32 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_32 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_32 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_32 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_32 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_32 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_32 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_33" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_33 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4</td>
<td headers="stub_1_33 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Aliments achetés au magasin</td>
<td headers="stub_1_33 an2010" class="gt_row gt_right">5,565</td>
<td headers="stub_1_33 an2019" class="gt_row gt_right">7,364</td>
<td headers="stub_1_33 an2021" class="gt_row gt_right">7,895</td>
<td headers="stub_1_33 diff_abs2019" class="gt_row gt_right">1,799</td>
<td headers="stub_1_33 diff_abs2021" class="gt_row gt_right">2,330</td>
<td headers="stub_1_33 diff_rel2019" class="gt_row gt_right">32.33%</td>
<td headers="stub_1_33 diff_rel2021" class="gt_row gt_right">41.87%</td>
<td headers="stub_1_33 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='9.99' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_34" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_34 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.5</td>
<td headers="stub_1_34 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Aliments achetés au restaurant</td>
<td headers="stub_1_34 an2010" class="gt_row gt_right">1,844</td>
<td headers="stub_1_34 an2019" class="gt_row gt_right">2,483</td>
<td headers="stub_1_34 an2021" class="gt_row gt_right">1,775</td>
<td headers="stub_1_34 diff_abs2019" class="gt_row gt_right">639</td>
<td headers="stub_1_34 diff_abs2021" class="gt_row gt_right">−69</td>
<td headers="stub_1_34 diff_rel2019" class="gt_row gt_right">34.65%</td>
<td headers="stub_1_34 diff_rel2021" class="gt_row gt_right">−3.74%</td>
<td headers="stub_1_34 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='10.71' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_35" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_35 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31</td>
<td headers="stub_1_35 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel de loisirs et services connexes</td>
<td headers="stub_1_35 an2010" class="gt_row gt_right">835</td>
<td headers="stub_1_35 an2019" class="gt_row gt_right">870</td>
<td headers="stub_1_35 an2021" class="gt_row gt_right">1,214</td>
<td headers="stub_1_35 diff_abs2019" class="gt_row gt_right">35</td>
<td headers="stub_1_35 diff_abs2021" class="gt_row gt_right">379</td>
<td headers="stub_1_35 diff_rel2019" class="gt_row gt_right">4.19%</td>
<td headers="stub_1_35 diff_rel2021" class="gt_row gt_right">45.39%</td>
<td headers="stub_1_35 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='1.30' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_36" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_36 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.32</td>
<td headers="stub_1_36 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel et services de divertissement au foyer</td>
<td headers="stub_1_36 an2010" class="gt_row gt_right">453</td>
<td headers="stub_1_36 an2019" class="gt_row gt_right">164</td>
<td headers="stub_1_36 an2021" class="gt_row gt_right">339</td>
<td headers="stub_1_36 diff_abs2019" class="gt_row gt_right">−289</td>
<td headers="stub_1_36 diff_abs2021" class="gt_row gt_right">−114</td>
<td headers="stub_1_36 diff_rel2019" class="gt_row gt_right">−63.80%</td>
<td headers="stub_1_36 diff_rel2021" class="gt_row gt_right">−25.17%</td>
<td headers="stub_1_36 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.49' y='0.89' width='19.71' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_37" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_37 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.33</td>
<td headers="stub_1_37 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de loisirs</td>
<td headers="stub_1_37 an2010" class="gt_row gt_right">1,359</td>
<td headers="stub_1_37 an2019" class="gt_row gt_right">2,126</td>
<td headers="stub_1_37 an2021" class="gt_row gt_right">1,131</td>
<td headers="stub_1_37 diff_abs2019" class="gt_row gt_right">767</td>
<td headers="stub_1_37 diff_abs2021" class="gt_row gt_right">−228</td>
<td headers="stub_1_37 diff_rel2019" class="gt_row gt_right">56.44%</td>
<td headers="stub_1_37 diff_rel2021" class="gt_row gt_right">−16.78%</td>
<td headers="stub_1_37 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='17.44' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_38" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_38 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.34</td>
<td headers="stub_1_38 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Véhicules récréatifs et services connexes</td>
<td headers="stub_1_38 an2010" class="gt_row gt_right">537</td>
<td headers="stub_1_38 an2019" class="gt_row gt_right">616</td>
<td headers="stub_1_38 an2021" class="gt_row gt_right">1,119</td>
<td headers="stub_1_38 diff_abs2019" class="gt_row gt_right">79</td>
<td headers="stub_1_38 diff_abs2021" class="gt_row gt_right">582</td>
<td headers="stub_1_38 diff_rel2019" class="gt_row gt_right">14.71%</td>
<td headers="stub_1_38 diff_rel2021" class="gt_row gt_right">108.38%</td>
<td headers="stub_1_38 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='4.55' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_39" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_39 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35.267</td>
<td headers="stub_1_39 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de scolarité</td>
<td headers="stub_1_39 an2010" class="gt_row gt_right">619</td>
<td headers="stub_1_39 an2019" class="gt_row gt_right">787</td>
<td headers="stub_1_39 an2021" class="gt_row gt_right">899</td>
<td headers="stub_1_39 diff_abs2019" class="gt_row gt_right">168</td>
<td headers="stub_1_39 diff_abs2021" class="gt_row gt_right">280</td>
<td headers="stub_1_39 diff_rel2019" class="gt_row gt_right">27.14%</td>
<td headers="stub_1_39 diff_rel2021" class="gt_row gt_right">45.23%</td>
<td headers="stub_1_39 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='8.39' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_40" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_40 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35.273</td>
<td headers="stub_1_40 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Manuels et fournitures scolaires</td>
<td headers="stub_1_40 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_40 an2019" class="gt_row gt_right">150</td>
<td headers="stub_1_40 an2021" class="gt_row gt_right">143</td>
<td headers="stub_1_40 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_40 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_40 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_40 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_40 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_41" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_41 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.359</td>
<td headers="stub_1_41 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits de tabac, boissons alcoolisées et cannabis pour usage non-thérapeutique</td>
<td headers="stub_1_41 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_41 an2019" class="gt_row gt_right">1,894</td>
<td headers="stub_1_41 an2021" class="gt_row gt_right">1,859</td>
<td headers="stub_1_41 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_41 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_41 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_41 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_41 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_42" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_42 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.274</td>
<td headers="stub_1_42 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Journaux</td>
<td headers="stub_1_42 an2010" class="gt_row gt_right">43</td>
<td headers="stub_1_42 an2019" class="gt_row gt_right">10</td>
<td headers="stub_1_42 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_42 diff_abs2019" class="gt_row gt_right">−33</td>
<td headers="stub_1_42 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_42 diff_rel2019" class="gt_row gt_right">−76.74%</td>
<td headers="stub_1_42 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_42 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.49' y='0.89' width='23.71' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_43" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_43 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.275</td>
<td headers="stub_1_43 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Revues et publications périodiques</td>
<td headers="stub_1_43 an2010" class="gt_row gt_right">32</td>
<td headers="stub_1_43 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_43 an2021" class="gt_row gt_right">7</td>
<td headers="stub_1_43 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_43 diff_abs2021" class="gt_row gt_right">−25</td>
<td headers="stub_1_43 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_43 diff_rel2021" class="gt_row gt_right">−78.12%</td>
<td headers="stub_1_43 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_44" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_44 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.276</td>
<td headers="stub_1_44 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Livres et livres numériques (sauf les manuels scolaires)</td>
<td headers="stub_1_44 an2010" class="gt_row gt_right">92</td>
<td headers="stub_1_44 an2019" class="gt_row gt_right">84</td>
<td headers="stub_1_44 an2021" class="gt_row gt_right">102</td>
<td headers="stub_1_44 diff_abs2019" class="gt_row gt_right">−8</td>
<td headers="stub_1_44 diff_abs2021" class="gt_row gt_right">10</td>
<td headers="stub_1_44 diff_rel2019" class="gt_row gt_right">−8.70%</td>
<td headers="stub_1_44 diff_rel2021" class="gt_row gt_right">10.87%</td>
<td headers="stub_1_44 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.52' y='0.89' width='2.69' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_45" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_45 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.277</td>
<td headers="stub_1_45 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cartes géographiques, partitions de musique et autres produits imprimés</td>
<td headers="stub_1_45 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_45 an2019" class="gt_row gt_right">7</td>
<td headers="stub_1_45 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_45 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_45 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_45 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_45 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_45 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_46" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_46 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.278</td>
<td headers="stub_1_46 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services reliés au matériel de lecture (e.g. reproduction, frais de bibliothèque)</td>
<td headers="stub_1_46 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_46 an2019" class="gt_row gt_right">14</td>
<td headers="stub_1_46 an2021" class="gt_row gt_right">17</td>
<td headers="stub_1_46 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_46 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_46 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_46 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_46 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_47" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_47 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.279</td>
<td headers="stub_1_47 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits de tabac et articles pour fumeurs</td>
<td headers="stub_1_47 an2010" class="gt_row gt_right">296</td>
<td headers="stub_1_47 an2019" class="gt_row gt_right">530</td>
<td headers="stub_1_47 an2021" class="gt_row gt_right">609</td>
<td headers="stub_1_47 diff_abs2019" class="gt_row gt_right">234</td>
<td headers="stub_1_47 diff_abs2021" class="gt_row gt_right">313</td>
<td headers="stub_1_47 diff_rel2019" class="gt_row gt_right">79.05%</td>
<td headers="stub_1_47 diff_rel2021" class="gt_row gt_right">105.74%</td>
<td headers="stub_1_47 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='24.42' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_48" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_48 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.282</td>
<td headers="stub_1_48 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Boissons alcoolisées</td>
<td headers="stub_1_48 an2010" class="gt_row gt_right">1,121</td>
<td headers="stub_1_48 an2019" class="gt_row gt_right">1,297</td>
<td headers="stub_1_48 an2021" class="gt_row gt_right">1,160</td>
<td headers="stub_1_48 diff_abs2019" class="gt_row gt_right">176</td>
<td headers="stub_1_48 diff_abs2021" class="gt_row gt_right">39</td>
<td headers="stub_1_48 diff_rel2019" class="gt_row gt_right">15.70%</td>
<td headers="stub_1_48 diff_rel2021" class="gt_row gt_right">3.48%</td>
<td headers="stub_1_48 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='4.85' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_49" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_49 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.361</td>
<td headers="stub_1_49 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cannabis pour usage non-thérapeutique</td>
<td headers="stub_1_49 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_49 an2019" class="gt_row gt_right">67</td>
<td headers="stub_1_49 an2021" class="gt_row gt_right">90</td>
<td headers="stub_1_49 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_49 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_49 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_49 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_49 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_50" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_50 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.38.286</td>
<td headers="stub_1_50 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Billets de loteries sous administration publique</td>
<td headers="stub_1_50 an2010" class="gt_row gt_right">130</td>
<td headers="stub_1_50 an2019" class="gt_row gt_right">149</td>
<td headers="stub_1_50 an2021" class="gt_row gt_right">136</td>
<td headers="stub_1_50 diff_abs2019" class="gt_row gt_right">19</td>
<td headers="stub_1_50 diff_abs2021" class="gt_row gt_right">6</td>
<td headers="stub_1_50 diff_rel2019" class="gt_row gt_right">14.62%</td>
<td headers="stub_1_50 diff_rel2021" class="gt_row gt_right">4.62%</td>
<td headers="stub_1_50 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='4.52' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_51" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_51 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.38.287</td>
<td headers="stub_1_51 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres jeux de hasard</td>
<td headers="stub_1_51 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_51 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_51 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_51 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_51 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_51 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_51 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_51 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_52" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_52 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.290</td>
<td headers="stub_1_52 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services financiers</td>
<td headers="stub_1_52 an2010" class="gt_row gt_right">266</td>
<td headers="stub_1_52 an2019" class="gt_row gt_right">489</td>
<td headers="stub_1_52 an2021" class="gt_row gt_right">467</td>
<td headers="stub_1_52 diff_abs2019" class="gt_row gt_right">223</td>
<td headers="stub_1_52 diff_abs2021" class="gt_row gt_right">201</td>
<td headers="stub_1_52 diff_rel2019" class="gt_row gt_right">83.83%</td>
<td headers="stub_1_52 diff_rel2021" class="gt_row gt_right">75.56%</td>
<td headers="stub_1_52 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='25.90' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_53" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_53 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295</td>
<td headers="stub_1_53 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres biens et services divers</td>
<td headers="stub_1_53 an2010" class="gt_row gt_right">787</td>
<td headers="stub_1_53 an2019" class="gt_row gt_right">932</td>
<td headers="stub_1_53 an2021" class="gt_row gt_right">1,177</td>
<td headers="stub_1_53 diff_abs2019" class="gt_row gt_right">145</td>
<td headers="stub_1_53 diff_abs2021" class="gt_row gt_right">390</td>
<td headers="stub_1_53 diff_rel2019" class="gt_row gt_right">18.42%</td>
<td headers="stub_1_53 diff_rel2021" class="gt_row gt_right">49.56%</td>
<td headers="stub_1_53 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='5.69' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_54" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_54 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6.11</td>
<td headers="stub_1_54 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres logements</td>
<td headers="stub_1_54 an2010" class="gt_row gt_right">866</td>
<td headers="stub_1_54 an2019" class="gt_row gt_right">1,366</td>
<td headers="stub_1_54 an2021" class="gt_row gt_right">1,112</td>
<td headers="stub_1_54 diff_abs2019" class="gt_row gt_right">500</td>
<td headers="stub_1_54 diff_abs2021" class="gt_row gt_right">246</td>
<td headers="stub_1_54 diff_rel2019" class="gt_row gt_right">57.74%</td>
<td headers="stub_1_54 diff_rel2021" class="gt_row gt_right">28.41%</td>
<td headers="stub_1_54 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='17.84' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_55" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_55 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6.7</td>
<td headers="stub_1_55 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Logement principal</td>
<td headers="stub_1_55 an2010" class="gt_row gt_right">11,156</td>
<td headers="stub_1_55 an2019" class="gt_row gt_right">14,455</td>
<td headers="stub_1_55 an2021" class="gt_row gt_right">14,770</td>
<td headers="stub_1_55 diff_abs2019" class="gt_row gt_right">3,299</td>
<td headers="stub_1_55 diff_abs2021" class="gt_row gt_right">3,614</td>
<td headers="stub_1_55 diff_rel2019" class="gt_row gt_right">29.57%</td>
<td headers="stub_1_55 diff_rel2021" class="gt_row gt_right">32.40%</td>
<td headers="stub_1_55 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='9.14' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_56" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_56 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.40</td>
<td headers="stub_1_56 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Impôts sur le revenu</td>
<td headers="stub_1_56 an2010" class="gt_row gt_right">10,130</td>
<td headers="stub_1_56 an2019" class="gt_row gt_right">15,030</td>
<td headers="stub_1_56 an2021" class="gt_row gt_right">16,342</td>
<td headers="stub_1_56 diff_abs2019" class="gt_row gt_right">4,900</td>
<td headers="stub_1_56 diff_abs2021" class="gt_row gt_right">6,212</td>
<td headers="stub_1_56 diff_rel2019" class="gt_row gt_right">48.37%</td>
<td headers="stub_1_56 diff_rel2021" class="gt_row gt_right">61.32%</td>
<td headers="stub_1_56 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='14.94' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_57" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_57 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.307</td>
<td headers="stub_1_57 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-emploi et d'assurance-parentale du Québec</td>
<td headers="stub_1_57 an2010" class="gt_row gt_right">417</td>
<td headers="stub_1_57 an2019" class="gt_row gt_right">756</td>
<td headers="stub_1_57 an2021" class="gt_row gt_right">709</td>
<td headers="stub_1_57 diff_abs2019" class="gt_row gt_right">339</td>
<td headers="stub_1_57 diff_abs2021" class="gt_row gt_right">292</td>
<td headers="stub_1_57 diff_rel2019" class="gt_row gt_right">81.29%</td>
<td headers="stub_1_57 diff_rel2021" class="gt_row gt_right">70.02%</td>
<td headers="stub_1_57 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='25.12' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_58" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_58 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.308</td>
<td headers="stub_1_58 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cotisations à des caisses de retraite ou de pension</td>
<td headers="stub_1_58 an2010" class="gt_row gt_right">2,529</td>
<td headers="stub_1_58 an2019" class="gt_row gt_right">3,775</td>
<td headers="stub_1_58 an2021" class="gt_row gt_right">4,126</td>
<td headers="stub_1_58 diff_abs2019" class="gt_row gt_right">1,246</td>
<td headers="stub_1_58 diff_abs2021" class="gt_row gt_right">1,597</td>
<td headers="stub_1_58 diff_rel2019" class="gt_row gt_right">49.27%</td>
<td headers="stub_1_58 diff_rel2021" class="gt_row gt_right">63.15%</td>
<td headers="stub_1_58 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='15.22' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_59" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_59 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.309</td>
<td headers="stub_1_59 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Contrats de rentes et argent transféré à des FERR</td>
<td headers="stub_1_59 an2010" class="gt_row gt_right">96</td>
<td headers="stub_1_59 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_59 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_59 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_59 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_59 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_59 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_59 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_60" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_60 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.310</td>
<td headers="stub_1_60 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-vie, d'assurances temporaires et d'assurances mixtes</td>
<td headers="stub_1_60 an2010" class="gt_row gt_right">587</td>
<td headers="stub_1_60 an2019" class="gt_row gt_right">656</td>
<td headers="stub_1_60 an2021" class="gt_row gt_right">587</td>
<td headers="stub_1_60 diff_abs2019" class="gt_row gt_right">69</td>
<td headers="stub_1_60 diff_abs2021" class="gt_row gt_right">0</td>
<td headers="stub_1_60 diff_rel2019" class="gt_row gt_right">11.75%</td>
<td headers="stub_1_60 diff_rel2021" class="gt_row gt_right">0.00%</td>
<td headers="stub_1_60 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='3.63' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_61" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_61 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311.312</td>
<td headers="stub_1_61 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux en argent à des personnes habitant au Canada</td>
<td headers="stub_1_61 an2010" class="gt_row gt_right">257</td>
<td headers="stub_1_61 an2019" class="gt_row gt_right">616</td>
<td headers="stub_1_61 an2021" class="gt_row gt_right">389</td>
<td headers="stub_1_61 diff_abs2019" class="gt_row gt_right">359</td>
<td headers="stub_1_61 diff_abs2021" class="gt_row gt_right">132</td>
<td headers="stub_1_61 diff_rel2019" class="gt_row gt_right">139.69%</td>
<td headers="stub_1_61 diff_rel2021" class="gt_row gt_right">51.36%</td>
<td headers="stub_1_61 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='43.16' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_62" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_62 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311.313</td>
<td headers="stub_1_62 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux en argent à des personnes habitant à l'extérieur du Canada</td>
<td headers="stub_1_62 an2010" class="gt_row gt_right">81</td>
<td headers="stub_1_62 an2019" class="gt_row gt_right">127</td>
<td headers="stub_1_62 an2021" class="gt_row gt_right">105</td>
<td headers="stub_1_62 diff_abs2019" class="gt_row gt_right">46</td>
<td headers="stub_1_62 diff_abs2021" class="gt_row gt_right">24</td>
<td headers="stub_1_62 diff_rel2019" class="gt_row gt_right">56.79%</td>
<td headers="stub_1_62 diff_rel2021" class="gt_row gt_right">29.63%</td>
<td headers="stub_1_62 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='17.55' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_63" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_63 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311.314</td>
<td headers="stub_1_63 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Pensions alimentaires</td>
<td headers="stub_1_63 an2010" class="gt_row gt_right">152</td>
<td headers="stub_1_63 an2019" class="gt_row gt_right">229</td>
<td headers="stub_1_63 an2021" class="gt_row gt_right">84</td>
<td headers="stub_1_63 diff_abs2019" class="gt_row gt_right">77</td>
<td headers="stub_1_63 diff_abs2021" class="gt_row gt_right">−68</td>
<td headers="stub_1_63 diff_rel2019" class="gt_row gt_right">50.66%</td>
<td headers="stub_1_63 diff_rel2021" class="gt_row gt_right">−44.74%</td>
<td headers="stub_1_63 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='15.65' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_64" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_64 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.315</td>
<td headers="stub_1_64 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dons de bienfaisance</td>
<td headers="stub_1_64 an2010" class="gt_row gt_right">255</td>
<td headers="stub_1_64 an2019" class="gt_row gt_right">244</td>
<td headers="stub_1_64 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_64 diff_abs2019" class="gt_row gt_right">−11</td>
<td headers="stub_1_64 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_64 diff_rel2019" class="gt_row gt_right">−4.31%</td>
<td headers="stub_1_64 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_64 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='27.87' y='0.89' width='1.33' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">Total</th>
<td headers="grand_summary_stub_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 an2010" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">62,769</td>
<td headers="grand_summary_stub_1 an2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">81,489</td>
<td headers="grand_summary_stub_1 an2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">81,949</td>
<td headers="grand_summary_stub_1 diff_abs2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">17,844</td>
<td headers="grand_summary_stub_1 diff_abs2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">19,342</td>
<td headers="grand_summary_stub_1 diff_rel2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 diff_rel2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 DUPE_COLUMN_PLT" class="gt_row gt_left gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::




voici aussi le top 5 "plus gross hausse" et "plus petit hausse pour la route.  


::: {.cell .column-screen-inset}

````{.cell-code}
```{{r}}
#| column: screen-inset

bind_rows(
  tableau_wide %>% 
    filter(!is.na(diff_rel2019) & (profondeur == 3 | (profondeur < 3 & last_profondeur==TRUE )))%>%
    arrange(diff_rel2019) %>%
    head(5),
  tableau_wide %>% 
    filter(!is.na(diff_rel2019) & (profondeur == 3 | (profondeur < 3 & last_profondeur==TRUE )))%>%
    arrange(diff_rel2019) %>%
    tail(5)
) %>% 
  select(-profondeur, -last_profondeur) %>% 
  gt::gt() %>%
  gt::cols_label(.list= setNames(as.list(names_with_spaces),names(tableau_wide%>% select(-profondeur, -last_profondeur)) )) %>%  ###  this is clever af simon!! quick tip to replace all "_" with " " in the column labels
  fmt_number(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), decimals = 0) %>%
  fmt_percent(columns = c(diff_rel2019, diff_rel2021)) %>% 
  gt::grand_summary_rows(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), 
                         fns = list(Total ~ sum(.,na.rm = TRUE)) ,
                         fmt = ~fmt_number(., decimals = 0)) %>%
  gt_plt_bar(column = diff_rel2019, keep_column = TRUE, color = cerulean_blue ) %>% 
  gt::sub_missing(missing_text = "-")
```
````

::: {.cell-output-display}


```{=html}
<div id="tkoivssmeb" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#tkoivssmeb table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#tkoivssmeb thead, #tkoivssmeb tbody, #tkoivssmeb tfoot, #tkoivssmeb tr, #tkoivssmeb td, #tkoivssmeb th {
  border-style: none;
}

#tkoivssmeb p {
  margin: 0;
  padding: 0;
}

#tkoivssmeb .gt_table {
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

#tkoivssmeb .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#tkoivssmeb .gt_title {
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

#tkoivssmeb .gt_subtitle {
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

#tkoivssmeb .gt_heading {
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

#tkoivssmeb .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#tkoivssmeb .gt_col_headings {
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

#tkoivssmeb .gt_col_heading {
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

#tkoivssmeb .gt_column_spanner_outer {
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

#tkoivssmeb .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#tkoivssmeb .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#tkoivssmeb .gt_column_spanner {
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

#tkoivssmeb .gt_spanner_row {
  border-bottom-style: hidden;
}

#tkoivssmeb .gt_group_heading {
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

#tkoivssmeb .gt_empty_group_heading {
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

#tkoivssmeb .gt_from_md > :first-child {
  margin-top: 0;
}

#tkoivssmeb .gt_from_md > :last-child {
  margin-bottom: 0;
}

#tkoivssmeb .gt_row {
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

#tkoivssmeb .gt_stub {
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

#tkoivssmeb .gt_stub_row_group {
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

#tkoivssmeb .gt_row_group_first td {
  border-top-width: 2px;
}

#tkoivssmeb .gt_row_group_first th {
  border-top-width: 2px;
}

#tkoivssmeb .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#tkoivssmeb .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#tkoivssmeb .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#tkoivssmeb .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#tkoivssmeb .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#tkoivssmeb .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#tkoivssmeb .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#tkoivssmeb .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#tkoivssmeb .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#tkoivssmeb .gt_footnotes {
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

#tkoivssmeb .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#tkoivssmeb .gt_sourcenotes {
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

#tkoivssmeb .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#tkoivssmeb .gt_left {
  text-align: left;
}

#tkoivssmeb .gt_center {
  text-align: center;
}

#tkoivssmeb .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#tkoivssmeb .gt_font_normal {
  font-weight: normal;
}

#tkoivssmeb .gt_font_bold {
  font-weight: bold;
}

#tkoivssmeb .gt_font_italic {
  font-style: italic;
}

#tkoivssmeb .gt_super {
  font-size: 65%;
}

#tkoivssmeb .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#tkoivssmeb .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#tkoivssmeb .gt_indent_1 {
  text-indent: 5px;
}

#tkoivssmeb .gt_indent_2 {
  text-indent: 10px;
}

#tkoivssmeb .gt_indent_3 {
  text-indent: 15px;
}

#tkoivssmeb .gt_indent_4 {
  text-indent: 20px;
}

#tkoivssmeb .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="hierarchie pour depenses des menages categories de niveau sommaire">hierarchie pour depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="depenses des menages categories de niveau sommaire">depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2010">an2010</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2019">an2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2021">an2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2019">diff abs2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2021">diff abs2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2019">diff rel2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2021">diff rel2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="diff_rel2019">diff_rel2019</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.274</td>
<td headers="stub_1_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Journaux</td>
<td headers="stub_1_1 an2010" class="gt_row gt_right">43</td>
<td headers="stub_1_1 an2019" class="gt_row gt_right">10</td>
<td headers="stub_1_1 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_1 diff_abs2019" class="gt_row gt_right">−33</td>
<td headers="stub_1_1 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_1 diff_rel2019" class="gt_row gt_right">−76.74%</td>
<td headers="stub_1_1 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_1 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.49' y='0.89' width='23.71' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_2 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.32</td>
<td headers="stub_1_2 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel et services de divertissement au foyer</td>
<td headers="stub_1_2 an2010" class="gt_row gt_right">453</td>
<td headers="stub_1_2 an2019" class="gt_row gt_right">164</td>
<td headers="stub_1_2 an2021" class="gt_row gt_right">339</td>
<td headers="stub_1_2 diff_abs2019" class="gt_row gt_right">−289</td>
<td headers="stub_1_2 diff_abs2021" class="gt_row gt_right">−114</td>
<td headers="stub_1_2 diff_rel2019" class="gt_row gt_right">−63.80%</td>
<td headers="stub_1_2 diff_rel2021" class="gt_row gt_right">−25.17%</td>
<td headers="stub_1_2 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.49' y='0.89' width='19.71' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_3 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.90</td>
<td headers="stub_1_3 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Aide domestique et autres services d'entretien ménager (sauf les services de garde)</td>
<td headers="stub_1_3 an2010" class="gt_row gt_right">236</td>
<td headers="stub_1_3 an2019" class="gt_row gt_right">157</td>
<td headers="stub_1_3 an2021" class="gt_row gt_right">155</td>
<td headers="stub_1_3 diff_abs2019" class="gt_row gt_right">−79</td>
<td headers="stub_1_3 diff_abs2021" class="gt_row gt_right">−81</td>
<td headers="stub_1_3 diff_rel2019" class="gt_row gt_right">−33.47%</td>
<td headers="stub_1_3 diff_rel2021" class="gt_row gt_right">−34.32%</td>
<td headers="stub_1_3 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='18.86' y='0.89' width='10.34' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_4 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.276</td>
<td headers="stub_1_4 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Livres et livres numériques (sauf les manuels scolaires)</td>
<td headers="stub_1_4 an2010" class="gt_row gt_right">92</td>
<td headers="stub_1_4 an2019" class="gt_row gt_right">84</td>
<td headers="stub_1_4 an2021" class="gt_row gt_right">102</td>
<td headers="stub_1_4 diff_abs2019" class="gt_row gt_right">−8</td>
<td headers="stub_1_4 diff_abs2021" class="gt_row gt_right">10</td>
<td headers="stub_1_4 diff_rel2019" class="gt_row gt_right">−8.70%</td>
<td headers="stub_1_4 diff_rel2021" class="gt_row gt_right">10.87%</td>
<td headers="stub_1_4 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='26.52' y='0.89' width='2.69' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_5" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_5 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.95</td>
<td headers="stub_1_5 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits et équipement de nettoyage</td>
<td headers="stub_1_5 an2010" class="gt_row gt_right">239</td>
<td headers="stub_1_5 an2019" class="gt_row gt_right">224</td>
<td headers="stub_1_5 an2021" class="gt_row gt_right">293</td>
<td headers="stub_1_5 diff_abs2019" class="gt_row gt_right">−15</td>
<td headers="stub_1_5 diff_abs2021" class="gt_row gt_right">54</td>
<td headers="stub_1_5 diff_rel2019" class="gt_row gt_right">−6.28%</td>
<td headers="stub_1_5 diff_rel2021" class="gt_row gt_right">22.59%</td>
<td headers="stub_1_5 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='27.26' y='0.89' width='1.94' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_6" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_6 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.290</td>
<td headers="stub_1_6 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services financiers</td>
<td headers="stub_1_6 an2010" class="gt_row gt_right">266</td>
<td headers="stub_1_6 an2019" class="gt_row gt_right">489</td>
<td headers="stub_1_6 an2021" class="gt_row gt_right">467</td>
<td headers="stub_1_6 diff_abs2019" class="gt_row gt_right">223</td>
<td headers="stub_1_6 diff_abs2021" class="gt_row gt_right">201</td>
<td headers="stub_1_6 diff_rel2019" class="gt_row gt_right">83.83%</td>
<td headers="stub_1_6 diff_rel2021" class="gt_row gt_right">75.56%</td>
<td headers="stub_1_6 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='25.90' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_7" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_7 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.203</td>
<td headers="stub_1_7 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes pour les régimes privés d'assurance-maladie</td>
<td headers="stub_1_7 an2010" class="gt_row gt_right">613</td>
<td headers="stub_1_7 an2019" class="gt_row gt_right">1,144</td>
<td headers="stub_1_7 an2021" class="gt_row gt_right">839</td>
<td headers="stub_1_7 diff_abs2019" class="gt_row gt_right">531</td>
<td headers="stub_1_7 diff_abs2021" class="gt_row gt_right">226</td>
<td headers="stub_1_7 diff_rel2019" class="gt_row gt_right">86.62%</td>
<td headers="stub_1_7 diff_rel2021" class="gt_row gt_right">36.87%</td>
<td headers="stub_1_7 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='26.76' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_8" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_8 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311.312</td>
<td headers="stub_1_8 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux en argent à des personnes habitant au Canada</td>
<td headers="stub_1_8 an2010" class="gt_row gt_right">257</td>
<td headers="stub_1_8 an2019" class="gt_row gt_right">616</td>
<td headers="stub_1_8 an2021" class="gt_row gt_right">389</td>
<td headers="stub_1_8 diff_abs2019" class="gt_row gt_right">359</td>
<td headers="stub_1_8 diff_abs2021" class="gt_row gt_right">132</td>
<td headers="stub_1_8 diff_rel2019" class="gt_row gt_right">139.69%</td>
<td headers="stub_1_8 diff_rel2021" class="gt_row gt_right">51.36%</td>
<td headers="stub_1_8 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='43.16' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_9" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_9 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.154</td>
<td headers="stub_1_9 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Tissus pour vêtements, fil à tricoter, fil et autres articles de couture</td>
<td headers="stub_1_9 an2010" class="gt_row gt_right">12</td>
<td headers="stub_1_9 an2019" class="gt_row gt_right">31</td>
<td headers="stub_1_9 an2021" class="gt_row gt_right">59</td>
<td headers="stub_1_9 diff_abs2019" class="gt_row gt_right">19</td>
<td headers="stub_1_9 diff_abs2021" class="gt_row gt_right">47</td>
<td headers="stub_1_9 diff_rel2019" class="gt_row gt_right">158.33%</td>
<td headers="stub_1_9 diff_rel2021" class="gt_row gt_right">391.67%</td>
<td headers="stub_1_9 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='48.92' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_10" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_10 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.155</td>
<td headers="stub_1_10 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services vestimentaires</td>
<td headers="stub_1_10 an2010" class="gt_row gt_right">36</td>
<td headers="stub_1_10 an2019" class="gt_row gt_right">123</td>
<td headers="stub_1_10 an2021" class="gt_row gt_right">90</td>
<td headers="stub_1_10 diff_abs2019" class="gt_row gt_right">87</td>
<td headers="stub_1_10 diff_abs2021" class="gt_row gt_right">54</td>
<td headers="stub_1_10 diff_rel2019" class="gt_row gt_right">241.67%</td>
<td headers="stub_1_10 diff_rel2021" class="gt_row gt_right">150.00%</td>
<td headers="stub_1_10 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='29.20' y='0.89' width='74.66' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='29.20' y1='14.17' x2='29.20' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">Total</th>
<td headers="grand_summary_stub_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 an2010" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">2,247</td>
<td headers="grand_summary_stub_1 an2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">3,042</td>
<td headers="grand_summary_stub_1 an2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">2,733</td>
<td headers="grand_summary_stub_1 diff_abs2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">795</td>
<td headers="grand_summary_stub_1 diff_abs2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">529</td>
<td headers="grand_summary_stub_1 diff_rel2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 diff_rel2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 DUPE_COLUMN_PLT" class="gt_row gt_left gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::



# profondeur 4   

J'ai même pas regardé, je génère au cas-où.  


::: {.cell .column-screen-inset}

````{.cell-code}
```{{r}}
#| column: screen-inset
tableau_wide %>% 
  filter(profondeur == 4 | (profondeur < 4 & last_profondeur==TRUE) )%>%
  select(-profondeur, -last_profondeur) %>% 
  gt::gt() %>%
  gt::cols_label(.list= setNames(as.list(names_with_spaces),names(tableau_wide %>% select(-profondeur, -last_profondeur)) )) %>%  ###  this is clever af simon!! quick tip to replace all "_" with " " in the column labels
  fmt_number(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), decimals = 0) %>%
  fmt_percent(columns = c(diff_rel2019, diff_rel2021)) %>% 
  gt::grand_summary_rows(columns = c(an2010, an2019, an2021, diff_abs2019, diff_abs2021), 
                         fns = list(Total ~ sum(.,na.rm = TRUE)) ,
                         fmt = ~fmt_number(., decimals = 0)) %>%
  gt_plt_bar(column = c(diff_rel2019), keep_column = TRUE, color = cerulean_blue )  %>% 
  gt::sub_missing(missing_text = "-")
```
````

::: {.cell-output-display}


```{=html}
<div id="jzjomsjvqq" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#jzjomsjvqq table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#jzjomsjvqq thead, #jzjomsjvqq tbody, #jzjomsjvqq tfoot, #jzjomsjvqq tr, #jzjomsjvqq td, #jzjomsjvqq th {
  border-style: none;
}

#jzjomsjvqq p {
  margin: 0;
  padding: 0;
}

#jzjomsjvqq .gt_table {
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

#jzjomsjvqq .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#jzjomsjvqq .gt_title {
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

#jzjomsjvqq .gt_subtitle {
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

#jzjomsjvqq .gt_heading {
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

#jzjomsjvqq .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#jzjomsjvqq .gt_col_headings {
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

#jzjomsjvqq .gt_col_heading {
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

#jzjomsjvqq .gt_column_spanner_outer {
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

#jzjomsjvqq .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#jzjomsjvqq .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#jzjomsjvqq .gt_column_spanner {
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

#jzjomsjvqq .gt_spanner_row {
  border-bottom-style: hidden;
}

#jzjomsjvqq .gt_group_heading {
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

#jzjomsjvqq .gt_empty_group_heading {
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

#jzjomsjvqq .gt_from_md > :first-child {
  margin-top: 0;
}

#jzjomsjvqq .gt_from_md > :last-child {
  margin-bottom: 0;
}

#jzjomsjvqq .gt_row {
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

#jzjomsjvqq .gt_stub {
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

#jzjomsjvqq .gt_stub_row_group {
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

#jzjomsjvqq .gt_row_group_first td {
  border-top-width: 2px;
}

#jzjomsjvqq .gt_row_group_first th {
  border-top-width: 2px;
}

#jzjomsjvqq .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#jzjomsjvqq .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#jzjomsjvqq .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#jzjomsjvqq .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#jzjomsjvqq .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#jzjomsjvqq .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#jzjomsjvqq .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#jzjomsjvqq .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#jzjomsjvqq .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#jzjomsjvqq .gt_footnotes {
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

#jzjomsjvqq .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#jzjomsjvqq .gt_sourcenotes {
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

#jzjomsjvqq .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#jzjomsjvqq .gt_left {
  text-align: left;
}

#jzjomsjvqq .gt_center {
  text-align: center;
}

#jzjomsjvqq .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#jzjomsjvqq .gt_font_normal {
  font-weight: normal;
}

#jzjomsjvqq .gt_font_bold {
  font-weight: bold;
}

#jzjomsjvqq .gt_font_italic {
  font-style: italic;
}

#jzjomsjvqq .gt_super {
  font-size: 65%;
}

#jzjomsjvqq .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#jzjomsjvqq .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#jzjomsjvqq .gt_indent_1 {
  text-indent: 5px;
}

#jzjomsjvqq .gt_indent_2 {
  text-indent: 10px;
}

#jzjomsjvqq .gt_indent_3 {
  text-indent: 15px;
}

#jzjomsjvqq .gt_indent_4 {
  text-indent: 20px;
}

#jzjomsjvqq .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="hierarchie pour depenses des menages categories de niveau sommaire">hierarchie pour depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="depenses des menages categories de niveau sommaire">depenses des menages categories de niveau sommaire</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2010">an2010</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2019">an2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="an2021">an2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2019">diff abs2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff abs2021">diff abs2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2019">diff rel2019</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="diff rel2021">diff rel2021</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="c(diff_rel2019)">c(diff_rel2019)</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><th id="stub_1_1" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.103.104</td>
<td headers="stub_1_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits de serre et de pépinière, fleurs coupées, plantes décoratives et graines de semence</td>
<td headers="stub_1_1 an2010" class="gt_row gt_right">130</td>
<td headers="stub_1_1 an2019" class="gt_row gt_right">162</td>
<td headers="stub_1_1 an2021" class="gt_row gt_right">137</td>
<td headers="stub_1_1 diff_abs2019" class="gt_row gt_right">32</td>
<td headers="stub_1_1 diff_abs2021" class="gt_row gt_right">7</td>
<td headers="stub_1_1 diff_rel2019" class="gt_row gt_right">24.62%</td>
<td headers="stub_1_1 diff_rel2021" class="gt_row gt_right">5.38%</td>
<td headers="stub_1_1 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.09' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_2" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_2 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.103.105</td>
<td headers="stub_1_2 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Engrais, désherbant, insecticides, pesticides, terreaux et conditionneur de sol</td>
<td headers="stub_1_2 an2010" class="gt_row gt_right">40</td>
<td headers="stub_1_2 an2019" class="gt_row gt_right">30</td>
<td headers="stub_1_2 an2021" class="gt_row gt_right">60</td>
<td headers="stub_1_2 diff_abs2019" class="gt_row gt_right">−10</td>
<td headers="stub_1_2 diff_abs2021" class="gt_row gt_right">20</td>
<td headers="stub_1_2 diff_rel2019" class="gt_row gt_right">−25.00%</td>
<td headers="stub_1_2 diff_rel2021" class="gt_row gt_right">50.00%</td>
<td headers="stub_1_2 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='8.27' y='0.89' width='1.11' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_3" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_3 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.103.106</td>
<td headers="stub_1_3 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services d'entretien du terrain, déneigement et enlèvement des déchets</td>
<td headers="stub_1_3 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_3 an2019" class="gt_row gt_right">225</td>
<td headers="stub_1_3 an2021" class="gt_row gt_right">206</td>
<td headers="stub_1_3 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_3 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_3 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_3 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_3 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_4" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_4 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.107</td>
<td headers="stub_1_4 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres accessoires pour la maison</td>
<td headers="stub_1_4 an2010" class="gt_row gt_right">95</td>
<td headers="stub_1_4 an2019" class="gt_row gt_right">134</td>
<td headers="stub_1_4 an2021" class="gt_row gt_right">153</td>
<td headers="stub_1_4 diff_abs2019" class="gt_row gt_right">39</td>
<td headers="stub_1_4 diff_abs2021" class="gt_row gt_right">58</td>
<td headers="stub_1_4 diff_rel2019" class="gt_row gt_right">41.05%</td>
<td headers="stub_1_4 diff_rel2021" class="gt_row gt_right">61.05%</td>
<td headers="stub_1_4 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.82' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_5" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_5 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.108.109</td>
<td headers="stub_1_5 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Garde d'enfants à l'extérieur du foyer</td>
<td headers="stub_1_5 an2010" class="gt_row gt_right">372</td>
<td headers="stub_1_5 an2019" class="gt_row gt_right">550</td>
<td headers="stub_1_5 an2021" class="gt_row gt_right">262</td>
<td headers="stub_1_5 diff_abs2019" class="gt_row gt_right">178</td>
<td headers="stub_1_5 diff_abs2021" class="gt_row gt_right">−110</td>
<td headers="stub_1_5 diff_rel2019" class="gt_row gt_right">47.85%</td>
<td headers="stub_1_5 diff_rel2021" class="gt_row gt_right">−29.57%</td>
<td headers="stub_1_5 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.12' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_6" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_6 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.108.110</td>
<td headers="stub_1_6 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Garde d'enfants à domicile (régulière et occasionnelle)</td>
<td headers="stub_1_6 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_6 an2019" class="gt_row gt_right">54</td>
<td headers="stub_1_6 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_6 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_6 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_6 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_6 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_6 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_7" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_7 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.13.324</td>
<td headers="stub_1_7 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services postaux, de messagerie, de livraison et autres services de communication</td>
<td headers="stub_1_7 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_7 an2019" class="gt_row gt_right">60</td>
<td headers="stub_1_7 an2021" class="gt_row gt_right">95</td>
<td headers="stub_1_7 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_7 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_7 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_7 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_7 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_8" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_8 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.13.83</td>
<td headers="stub_1_8 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Téléphone</td>
<td headers="stub_1_8 an2010" class="gt_row gt_right">973</td>
<td headers="stub_1_8 an2019" class="gt_row gt_right">1,306</td>
<td headers="stub_1_8 an2021" class="gt_row gt_right">1,383</td>
<td headers="stub_1_8 diff_abs2019" class="gt_row gt_right">333</td>
<td headers="stub_1_8 diff_abs2021" class="gt_row gt_right">410</td>
<td headers="stub_1_8 diff_rel2019" class="gt_row gt_right">34.22%</td>
<td headers="stub_1_8 diff_rel2021" class="gt_row gt_right">42.14%</td>
<td headers="stub_1_8 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.52' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_9" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_9 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.13.87</td>
<td headers="stub_1_9 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services d'accès à Internet</td>
<td headers="stub_1_9 an2010" class="gt_row gt_right">358</td>
<td headers="stub_1_9 an2019" class="gt_row gt_right">620</td>
<td headers="stub_1_9 an2021" class="gt_row gt_right">741</td>
<td headers="stub_1_9 diff_abs2019" class="gt_row gt_right">262</td>
<td headers="stub_1_9 diff_abs2021" class="gt_row gt_right">383</td>
<td headers="stub_1_9 diff_rel2019" class="gt_row gt_right">73.18%</td>
<td headers="stub_1_9 diff_rel2021" class="gt_row gt_right">106.98%</td>
<td headers="stub_1_9 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.24' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_10" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_10 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.13.88</td>
<td headers="stub_1_10 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services numériques</td>
<td headers="stub_1_10 an2010" class="gt_row gt_right">4</td>
<td headers="stub_1_10 an2019" class="gt_row gt_right">89</td>
<td headers="stub_1_10 an2021" class="gt_row gt_right">123</td>
<td headers="stub_1_10 diff_abs2019" class="gt_row gt_right">85</td>
<td headers="stub_1_10 diff_abs2021" class="gt_row gt_right">119</td>
<td headers="stub_1_10 diff_rel2019" class="gt_row gt_right">2,125.00%</td>
<td headers="stub_1_10 diff_rel2021" class="gt_row gt_right">2,975.00%</td>
<td headers="stub_1_10 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='94.10' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_11" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_11 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.13.89</td>
<td headers="stub_1_11 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services postaux, de messagerie et autres services de communication</td>
<td headers="stub_1_11 an2010" class="gt_row gt_right">31</td>
<td headers="stub_1_11 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_11 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_11 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_11 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_11 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_11 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_11 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_12" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_12 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.90</td>
<td headers="stub_1_12 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Aide domestique et autres services d'entretien ménager (sauf les services de garde)</td>
<td headers="stub_1_12 an2010" class="gt_row gt_right">236</td>
<td headers="stub_1_12 an2019" class="gt_row gt_right">157</td>
<td headers="stub_1_12 an2021" class="gt_row gt_right">155</td>
<td headers="stub_1_12 diff_abs2019" class="gt_row gt_right">−79</td>
<td headers="stub_1_12 diff_abs2021" class="gt_row gt_right">−81</td>
<td headers="stub_1_12 diff_rel2019" class="gt_row gt_right">−33.47%</td>
<td headers="stub_1_12 diff_rel2021" class="gt_row gt_right">−34.32%</td>
<td headers="stub_1_12 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='7.90' y='0.89' width='1.48' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_13" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_13 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.91.365</td>
<td headers="stub_1_13 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Nourriture et articles pour animaux domestiques</td>
<td headers="stub_1_13 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_13 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_13 an2021" class="gt_row gt_right">264</td>
<td headers="stub_1_13 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_13 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_13 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_13 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_13 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_14" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_14 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.91.366</td>
<td headers="stub_1_14 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Achats d'animaux domestiques</td>
<td headers="stub_1_14 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_14 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_14 an2021" class="gt_row gt_right">62</td>
<td headers="stub_1_14 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_14 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_14 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_14 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_14 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_15" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_15 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.91.92</td>
<td headers="stub_1_15 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Nourriture pour animaux domestiques</td>
<td headers="stub_1_15 an2010" class="gt_row gt_right">176</td>
<td headers="stub_1_15 an2019" class="gt_row gt_right">154</td>
<td headers="stub_1_15 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_15 diff_abs2019" class="gt_row gt_right">−22</td>
<td headers="stub_1_15 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_15 diff_rel2019" class="gt_row gt_right">−12.50%</td>
<td headers="stub_1_15 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_15 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='8.83' y='0.89' width='0.55' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_16" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_16 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.91.93</td>
<td headers="stub_1_16 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Achats d'animaux domestiques et accessoires</td>
<td headers="stub_1_16 an2010" class="gt_row gt_right">91</td>
<td headers="stub_1_16 an2019" class="gt_row gt_right">119</td>
<td headers="stub_1_16 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_16 diff_abs2019" class="gt_row gt_right">28</td>
<td headers="stub_1_16 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_16 diff_rel2019" class="gt_row gt_right">30.77%</td>
<td headers="stub_1_16 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_16 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.36' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_17" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_17 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.91.94</td>
<td headers="stub_1_17 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Soins vétérinaires et autres services animaliers</td>
<td headers="stub_1_17 an2010" class="gt_row gt_right">117</td>
<td headers="stub_1_17 an2019" class="gt_row gt_right">179</td>
<td headers="stub_1_17 an2021" class="gt_row gt_right">193</td>
<td headers="stub_1_17 diff_abs2019" class="gt_row gt_right">62</td>
<td headers="stub_1_17 diff_abs2021" class="gt_row gt_right">76</td>
<td headers="stub_1_17 diff_rel2019" class="gt_row gt_right">52.99%</td>
<td headers="stub_1_17 diff_rel2021" class="gt_row gt_right">64.96%</td>
<td headers="stub_1_17 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.35' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_18" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_18 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.95.96</td>
<td headers="stub_1_18 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Détergents et autres savons</td>
<td headers="stub_1_18 an2010" class="gt_row gt_right">106</td>
<td headers="stub_1_18 an2019" class="gt_row gt_right">102</td>
<td headers="stub_1_18 an2021" class="gt_row gt_right">103</td>
<td headers="stub_1_18 diff_abs2019" class="gt_row gt_right">−4</td>
<td headers="stub_1_18 diff_abs2021" class="gt_row gt_right">−3</td>
<td headers="stub_1_18 diff_rel2019" class="gt_row gt_right">−3.77%</td>
<td headers="stub_1_18 diff_rel2021" class="gt_row gt_right">−2.83%</td>
<td headers="stub_1_18 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.21' y='0.89' width='0.17' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_19" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_19 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.95.97</td>
<td headers="stub_1_19 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres produits ménagers de nettoyage</td>
<td headers="stub_1_19 an2010" class="gt_row gt_right">111</td>
<td headers="stub_1_19 an2019" class="gt_row gt_right">104</td>
<td headers="stub_1_19 an2021" class="gt_row gt_right">164</td>
<td headers="stub_1_19 diff_abs2019" class="gt_row gt_right">−7</td>
<td headers="stub_1_19 diff_abs2021" class="gt_row gt_right">53</td>
<td headers="stub_1_19 diff_rel2019" class="gt_row gt_right">−6.31%</td>
<td headers="stub_1_19 diff_rel2021" class="gt_row gt_right">47.75%</td>
<td headers="stub_1_19 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.10' y='0.89' width='0.28' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_20" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_20 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.95.98</td>
<td headers="stub_1_20 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Équipement d'entretien ménager (non-électrique)</td>
<td headers="stub_1_20 an2010" class="gt_row gt_right">22</td>
<td headers="stub_1_20 an2019" class="gt_row gt_right">18</td>
<td headers="stub_1_20 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_20 diff_abs2019" class="gt_row gt_right">−4</td>
<td headers="stub_1_20 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_20 diff_rel2019" class="gt_row gt_right">−18.18%</td>
<td headers="stub_1_20 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_20 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='8.58' y='0.89' width='0.81' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_21" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_21 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.99.100</td>
<td headers="stub_1_21 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Papeterie (sauf les fournitures scolaires)</td>
<td headers="stub_1_21 an2010" class="gt_row gt_right">104</td>
<td headers="stub_1_21 an2019" class="gt_row gt_right">110</td>
<td headers="stub_1_21 an2021" class="gt_row gt_right">143</td>
<td headers="stub_1_21 diff_abs2019" class="gt_row gt_right">6</td>
<td headers="stub_1_21 diff_abs2021" class="gt_row gt_right">39</td>
<td headers="stub_1_21 diff_rel2019" class="gt_row gt_right">5.77%</td>
<td headers="stub_1_21 diff_rel2021" class="gt_row gt_right">37.50%</td>
<td headers="stub_1_21 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.26' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_22" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_22 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.99.101</td>
<td headers="stub_1_22 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres articles en papier</td>
<td headers="stub_1_22 an2010" class="gt_row gt_right">165</td>
<td headers="stub_1_22 an2019" class="gt_row gt_right">171</td>
<td headers="stub_1_22 an2021" class="gt_row gt_right">193</td>
<td headers="stub_1_22 diff_abs2019" class="gt_row gt_right">6</td>
<td headers="stub_1_22 diff_abs2021" class="gt_row gt_right">28</td>
<td headers="stub_1_22 diff_rel2019" class="gt_row gt_right">3.64%</td>
<td headers="stub_1_22 diff_rel2021" class="gt_row gt_right">16.97%</td>
<td headers="stub_1_22 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.16' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_23" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_23 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.12.99.102</td>
<td headers="stub_1_23 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Articles en plastique et en aluminium</td>
<td headers="stub_1_23 an2010" class="gt_row gt_right">49</td>
<td headers="stub_1_23 an2019" class="gt_row gt_right">53</td>
<td headers="stub_1_23 an2021" class="gt_row gt_right">60</td>
<td headers="stub_1_23 diff_abs2019" class="gt_row gt_right">4</td>
<td headers="stub_1_23 diff_abs2021" class="gt_row gt_right">11</td>
<td headers="stub_1_23 diff_rel2019" class="gt_row gt_right">8.16%</td>
<td headers="stub_1_23 diff_rel2021" class="gt_row gt_right">22.45%</td>
<td headers="stub_1_23 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.36' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_24" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_24 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.128</td>
<td headers="stub_1_24 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Entretien, location, réparations et services reliés à l'ameublement et à l'équipement ménager</td>
<td headers="stub_1_24 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_24 an2019" class="gt_row gt_right">41</td>
<td headers="stub_1_24 an2021" class="gt_row gt_right">117</td>
<td headers="stub_1_24 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_24 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_24 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_24 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_24 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_25" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_25 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.129.130</td>
<td headers="stub_1_25 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Location de matériel de chauffage</td>
<td headers="stub_1_25 an2010" class="gt_row gt_right">7</td>
<td headers="stub_1_25 an2019" class="gt_row gt_right">11</td>
<td headers="stub_1_25 an2021" class="gt_row gt_right">16</td>
<td headers="stub_1_25 diff_abs2019" class="gt_row gt_right">4</td>
<td headers="stub_1_25 diff_abs2021" class="gt_row gt_right">9</td>
<td headers="stub_1_25 diff_rel2019" class="gt_row gt_right">57.14%</td>
<td headers="stub_1_25 diff_rel2021" class="gt_row gt_right">128.57%</td>
<td headers="stub_1_25 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.53' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_26" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_26 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.129.131</td>
<td headers="stub_1_26 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de sécurité résidentielle</td>
<td headers="stub_1_26 an2010" class="gt_row gt_right">33</td>
<td headers="stub_1_26 an2019" class="gt_row gt_right">33</td>
<td headers="stub_1_26 an2021" class="gt_row gt_right">37</td>
<td headers="stub_1_26 diff_abs2019" class="gt_row gt_right">0</td>
<td headers="stub_1_26 diff_abs2021" class="gt_row gt_right">4</td>
<td headers="stub_1_26 diff_rel2019" class="gt_row gt_right">0.00%</td>
<td headers="stub_1_26 diff_rel2021" class="gt_row gt_right">12.12%</td>
<td headers="stub_1_26 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.00' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_27" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_27 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.15.111</td>
<td headers="stub_1_27 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Meubles</td>
<td headers="stub_1_27 an2010" class="gt_row gt_right">474</td>
<td headers="stub_1_27 an2019" class="gt_row gt_right">635</td>
<td headers="stub_1_27 an2021" class="gt_row gt_right">937</td>
<td headers="stub_1_27 diff_abs2019" class="gt_row gt_right">161</td>
<td headers="stub_1_27 diff_abs2021" class="gt_row gt_right">463</td>
<td headers="stub_1_27 diff_rel2019" class="gt_row gt_right">33.97%</td>
<td headers="stub_1_27 diff_rel2021" class="gt_row gt_right">97.68%</td>
<td headers="stub_1_27 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.50' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_28" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_28 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.15.112</td>
<td headers="stub_1_28 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Carpettes, tapis et sous-tapis</td>
<td headers="stub_1_28 an2010" class="gt_row gt_right">23</td>
<td headers="stub_1_28 an2019" class="gt_row gt_right">20</td>
<td headers="stub_1_28 an2021" class="gt_row gt_right">37</td>
<td headers="stub_1_28 diff_abs2019" class="gt_row gt_right">−3</td>
<td headers="stub_1_28 diff_abs2021" class="gt_row gt_right">14</td>
<td headers="stub_1_28 diff_rel2019" class="gt_row gt_right">−13.04%</td>
<td headers="stub_1_28 diff_rel2021" class="gt_row gt_right">60.87%</td>
<td headers="stub_1_28 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='8.80' y='0.89' width='0.58' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_29" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_29 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.15.113</td>
<td headers="stub_1_29 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Oeuvres d'art, antiquités et articles décoratifs</td>
<td headers="stub_1_29 an2010" class="gt_row gt_right">57</td>
<td headers="stub_1_29 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_29 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_29 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_29 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_29 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_29 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_29 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_30" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_30 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.15.114</td>
<td headers="stub_1_30 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Linges de maison</td>
<td headers="stub_1_30 an2010" class="gt_row gt_right">46</td>
<td headers="stub_1_30 an2019" class="gt_row gt_right">88</td>
<td headers="stub_1_30 an2021" class="gt_row gt_right">113</td>
<td headers="stub_1_30 diff_abs2019" class="gt_row gt_right">42</td>
<td headers="stub_1_30 diff_abs2021" class="gt_row gt_right">67</td>
<td headers="stub_1_30 diff_rel2019" class="gt_row gt_right">91.30%</td>
<td headers="stub_1_30 diff_rel2021" class="gt_row gt_right">145.65%</td>
<td headers="stub_1_30 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='4.04' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_31" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_31 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.15.115</td>
<td headers="stub_1_31 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autre ameublement pour la maison (rideaux, miroirs et cadres pour photographies)</td>
<td headers="stub_1_31 an2010" class="gt_row gt_right">116</td>
<td headers="stub_1_31 an2019" class="gt_row gt_right">82</td>
<td headers="stub_1_31 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_31 diff_abs2019" class="gt_row gt_right">−34</td>
<td headers="stub_1_31 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_31 diff_rel2019" class="gt_row gt_right">−29.31%</td>
<td headers="stub_1_31 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_31 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='8.08' y='0.89' width='1.30' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_32" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_32 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.15.325</td>
<td headers="stub_1_32 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Oeuvres d'art, sculptures et autres articles décoratifs</td>
<td headers="stub_1_32 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_32 an2019" class="gt_row gt_right">55</td>
<td headers="stub_1_32 an2021" class="gt_row gt_right">134</td>
<td headers="stub_1_32 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_32 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_32 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_32 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_32 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_33" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_33 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.16.123</td>
<td headers="stub_1_33 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autre équipement ménager</td>
<td headers="stub_1_33 an2010" class="gt_row gt_right">461</td>
<td headers="stub_1_33 an2019" class="gt_row gt_right">516</td>
<td headers="stub_1_33 an2021" class="gt_row gt_right">844</td>
<td headers="stub_1_33 diff_abs2019" class="gt_row gt_right">55</td>
<td headers="stub_1_33 diff_abs2021" class="gt_row gt_right">383</td>
<td headers="stub_1_33 diff_rel2019" class="gt_row gt_right">11.93%</td>
<td headers="stub_1_33 diff_rel2021" class="gt_row gt_right">83.08%</td>
<td headers="stub_1_33 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.53' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_34" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_34 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.14.16.17</td>
<td headers="stub_1_34 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Appareils électroménagers</td>
<td headers="stub_1_34 an2010" class="gt_row gt_right">376</td>
<td headers="stub_1_34 an2019" class="gt_row gt_right">617</td>
<td headers="stub_1_34 an2021" class="gt_row gt_right">718</td>
<td headers="stub_1_34 diff_abs2019" class="gt_row gt_right">241</td>
<td headers="stub_1_34 diff_abs2021" class="gt_row gt_right">342</td>
<td headers="stub_1_34 diff_rel2019" class="gt_row gt_right">64.10%</td>
<td headers="stub_1_34 diff_rel2021" class="gt_row gt_right">90.96%</td>
<td headers="stub_1_34 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.84' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_35" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_35 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.132.133</td>
<td headers="stub_1_35 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements (femmes et filles âgées de 4 ans et plus)</td>
<td headers="stub_1_35 an2010" class="gt_row gt_right">1,226</td>
<td headers="stub_1_35 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_35 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_35 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_35 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_35 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_35 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_35 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_36" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_36 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.132.134</td>
<td headers="stub_1_36 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Chaussures (femmes et filles âgées de 4 ans et plus)</td>
<td headers="stub_1_36 an2010" class="gt_row gt_right">309</td>
<td headers="stub_1_36 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_36 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_36 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_36 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_36 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_36 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_36 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_37" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_37 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.132.137</td>
<td headers="stub_1_37 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Accessoires (femmes et filles âgées de 4 ans et plus)</td>
<td headers="stub_1_37 an2010" class="gt_row gt_right">77</td>
<td headers="stub_1_37 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_37 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_37 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_37 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_37 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_37 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_37 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_38" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_38 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.132.138</td>
<td headers="stub_1_38 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Montres et bijoux (femmes et filles âgées de 4 ans et plus)</td>
<td headers="stub_1_38 an2010" class="gt_row gt_right">92</td>
<td headers="stub_1_38 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_38 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_38 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_38 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_38 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_38 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_38 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_39" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_39 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.132.329</td>
<td headers="stub_1_39 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements (femmes et filles âgées de 14 ans et plus)</td>
<td headers="stub_1_39 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_39 an2019" class="gt_row gt_right">985</td>
<td headers="stub_1_39 an2021" class="gt_row gt_right">599</td>
<td headers="stub_1_39 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_39 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_39 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_39 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_39 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_40" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_40 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.132.330</td>
<td headers="stub_1_40 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Chaussures (femmes et filles âgées de 14 ans et plus)</td>
<td headers="stub_1_40 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_40 an2019" class="gt_row gt_right">257</td>
<td headers="stub_1_40 an2021" class="gt_row gt_right">231</td>
<td headers="stub_1_40 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_40 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_40 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_40 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_40 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_41" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_41 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.141.142</td>
<td headers="stub_1_41 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements (hommes et garçons âgés de 4 ans et plus)</td>
<td headers="stub_1_41 an2010" class="gt_row gt_right">777</td>
<td headers="stub_1_41 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_41 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_41 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_41 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_41 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_41 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_41 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_42" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_42 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.141.143</td>
<td headers="stub_1_42 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Chaussures (hommes et garçons âgés de 4 ans et plus)</td>
<td headers="stub_1_42 an2010" class="gt_row gt_right">190</td>
<td headers="stub_1_42 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_42 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_42 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_42 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_42 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_42 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_42 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_43" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_43 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.141.146</td>
<td headers="stub_1_43 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Accessoires (hommes et garçons âgés de 4 ans et plus)</td>
<td headers="stub_1_43 an2010" class="gt_row gt_right">29</td>
<td headers="stub_1_43 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_43 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_43 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_43 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_43 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_43 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_43 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_44" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_44 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.141.147</td>
<td headers="stub_1_44 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Montres et bijoux (hommes et garçons âgés de 4 ans et plus)</td>
<td headers="stub_1_44 an2010" class="gt_row gt_right">54</td>
<td headers="stub_1_44 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_44 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_44 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_44 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_44 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_44 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_44 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_45" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_45 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.141.332</td>
<td headers="stub_1_45 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements (hommes et garçons âgés de 14 ans et plus)</td>
<td headers="stub_1_45 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_45 an2019" class="gt_row gt_right">677</td>
<td headers="stub_1_45 an2021" class="gt_row gt_right">354</td>
<td headers="stub_1_45 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_45 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_45 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_45 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_45 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_46" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_46 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.141.333</td>
<td headers="stub_1_46 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Chaussures (hommes et garçons âgés de 14 ans et plus)</td>
<td headers="stub_1_46 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_46 an2019" class="gt_row gt_right">156</td>
<td headers="stub_1_46 an2021" class="gt_row gt_right">187</td>
<td headers="stub_1_46 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_46 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_46 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_46 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_46 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_47" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_47 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.150.151</td>
<td headers="stub_1_47 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements et couches en tissu (enfants âgés de moins de 4 ans)</td>
<td headers="stub_1_47 an2010" class="gt_row gt_right">64</td>
<td headers="stub_1_47 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_47 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_47 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_47 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_47 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_47 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_47 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_48" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_48 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.150.152</td>
<td headers="stub_1_48 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Chaussures (enfants âgés de moins de 4 ans)</td>
<td headers="stub_1_48 an2010" class="gt_row gt_right">15</td>
<td headers="stub_1_48 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_48 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_48 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_48 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_48 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_48 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_48 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_49" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_49 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.150.335</td>
<td headers="stub_1_49 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements et couches en tissu (enfants âgés de moins de 14 ans)</td>
<td headers="stub_1_49 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_49 an2019" class="gt_row gt_right">307</td>
<td headers="stub_1_49 an2021" class="gt_row gt_right">202</td>
<td headers="stub_1_49 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_49 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_49 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_49 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_49 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_50" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_50 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.150.336</td>
<td headers="stub_1_50 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Chaussures (enfants âgés de moins de 14 ans)</td>
<td headers="stub_1_50 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_50 an2019" class="gt_row gt_right">71</td>
<td headers="stub_1_50 an2021" class="gt_row gt_right">89</td>
<td headers="stub_1_50 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_50 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_50 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_50 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_50 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_51" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_51 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.153</td>
<td headers="stub_1_51 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux de vêtements à des personnes autres que les membres du ménage</td>
<td headers="stub_1_51 an2010" class="gt_row gt_right">290</td>
<td headers="stub_1_51 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_51 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_51 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_51 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_51 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_51 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_51 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_52" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_52 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.154</td>
<td headers="stub_1_52 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Tissus pour vêtements, fil à tricoter, fil et autres articles de couture</td>
<td headers="stub_1_52 an2010" class="gt_row gt_right">12</td>
<td headers="stub_1_52 an2019" class="gt_row gt_right">31</td>
<td headers="stub_1_52 an2021" class="gt_row gt_right">59</td>
<td headers="stub_1_52 diff_abs2019" class="gt_row gt_right">19</td>
<td headers="stub_1_52 diff_abs2021" class="gt_row gt_right">47</td>
<td headers="stub_1_52 diff_rel2019" class="gt_row gt_right">158.33%</td>
<td headers="stub_1_52 diff_rel2021" class="gt_row gt_right">391.67%</td>
<td headers="stub_1_52 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='7.01' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_53" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_53 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.155.156</td>
<td headers="stub_1_53 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de blanchisserie et de nettoyage à sec</td>
<td headers="stub_1_53 an2010" class="gt_row gt_right">12</td>
<td headers="stub_1_53 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_53 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_53 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_53 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_53 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_53 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_53 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_54" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_54 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.155.157</td>
<td headers="stub_1_54 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Buanderie et nettoyage à sec libre-service</td>
<td headers="stub_1_54 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_54 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_54 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_54 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_54 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_54 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_54 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_54 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_55" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_55 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.155.158</td>
<td headers="stub_1_55 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de couturier, de cordonnier et de bijoutier</td>
<td headers="stub_1_55 an2010" class="gt_row gt_right">18</td>
<td headers="stub_1_55 an2019" class="gt_row gt_right">56</td>
<td headers="stub_1_55 an2021" class="gt_row gt_right">46</td>
<td headers="stub_1_55 diff_abs2019" class="gt_row gt_right">38</td>
<td headers="stub_1_55 diff_abs2021" class="gt_row gt_right">28</td>
<td headers="stub_1_55 diff_rel2019" class="gt_row gt_right">211.11%</td>
<td headers="stub_1_55 diff_rel2021" class="gt_row gt_right">155.56%</td>
<td headers="stub_1_55 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='9.35' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_56" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_56 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.155.340</td>
<td headers="stub_1_56 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Buanderie, services de nettoyage à sec et de blanchisserie</td>
<td headers="stub_1_56 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_56 an2019" class="gt_row gt_right">67</td>
<td headers="stub_1_56 an2021" class="gt_row gt_right">44</td>
<td headers="stub_1_56 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_56 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_56 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_56 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_56 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_57" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_57 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.328</td>
<td headers="stub_1_57 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour femmes et filles (femmes et filles âgées de 14 ans et plus)</td>
<td headers="stub_1_57 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_57 an2019" class="gt_row gt_right">1,242</td>
<td headers="stub_1_57 an2021" class="gt_row gt_right">830</td>
<td headers="stub_1_57 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_57 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_57 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_57 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_57 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_58" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_58 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.331</td>
<td headers="stub_1_58 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour hommes et garçons (hommes et garçons âgés de 14 ans et plus)</td>
<td headers="stub_1_58 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_58 an2019" class="gt_row gt_right">833</td>
<td headers="stub_1_58 an2021" class="gt_row gt_right">541</td>
<td headers="stub_1_58 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_58 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_58 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_58 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_58 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_59" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_59 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.334</td>
<td headers="stub_1_59 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Vêtements pour enfants (enfants âgés de moins de 14 ans)</td>
<td headers="stub_1_59 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_59 an2019" class="gt_row gt_right">379</td>
<td headers="stub_1_59 an2021" class="gt_row gt_right">291</td>
<td headers="stub_1_59 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_59 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_59 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_59 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_59 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_60" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_60 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.337</td>
<td headers="stub_1_60 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Chaussures de sport</td>
<td headers="stub_1_60 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_60 an2019" class="gt_row gt_right">140</td>
<td headers="stub_1_60 an2021" class="gt_row gt_right">146</td>
<td headers="stub_1_60 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_60 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_60 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_60 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_60 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_61" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_61 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.338</td>
<td headers="stub_1_61 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Accessoires</td>
<td headers="stub_1_61 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_61 an2019" class="gt_row gt_right">139</td>
<td headers="stub_1_61 an2021" class="gt_row gt_right">130</td>
<td headers="stub_1_61 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_61 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_61 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_61 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_61 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_62" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_62 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.18.339</td>
<td headers="stub_1_62 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Montres et bijoux</td>
<td headers="stub_1_62 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_62 an2019" class="gt_row gt_right">127</td>
<td headers="stub_1_62 an2021" class="gt_row gt_right">97</td>
<td headers="stub_1_62 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_62 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_62 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_62 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_62 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_63" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_63 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.24.159</td>
<td headers="stub_1_63 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Automobiles, fourgonnettes et camions à usage privé</td>
<td headers="stub_1_63 an2010" class="gt_row gt_right">5,187</td>
<td headers="stub_1_63 an2019" class="gt_row gt_right">4,963</td>
<td headers="stub_1_63 an2021" class="gt_row gt_right">4,805</td>
<td headers="stub_1_63 diff_abs2019" class="gt_row gt_right">−224</td>
<td headers="stub_1_63 diff_abs2021" class="gt_row gt_right">−382</td>
<td headers="stub_1_63 diff_rel2019" class="gt_row gt_right">−4.32%</td>
<td headers="stub_1_63 diff_rel2021" class="gt_row gt_right">−7.36%</td>
<td headers="stub_1_63 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.19' y='0.89' width='0.19' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_64" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_64 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.24.170</td>
<td headers="stub_1_64 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Automobiles, fourgonnettes et camions de location</td>
<td headers="stub_1_64 an2010" class="gt_row gt_right">36</td>
<td headers="stub_1_64 an2019" class="gt_row gt_right">48</td>
<td headers="stub_1_64 an2021" class="gt_row gt_right">33</td>
<td headers="stub_1_64 diff_abs2019" class="gt_row gt_right">12</td>
<td headers="stub_1_64 diff_abs2021" class="gt_row gt_right">−3</td>
<td headers="stub_1_64 diff_rel2019" class="gt_row gt_right">33.33%</td>
<td headers="stub_1_64 diff_rel2021" class="gt_row gt_right">−8.33%</td>
<td headers="stub_1_64 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.48' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_65" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_65 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.24.171</td>
<td headers="stub_1_65 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Utilisation d'automobiles, de fourgonnettes et de camions</td>
<td headers="stub_1_65 an2010" class="gt_row gt_right">4,050</td>
<td headers="stub_1_65 an2019" class="gt_row gt_right">4,499</td>
<td headers="stub_1_65 an2021" class="gt_row gt_right">4,141</td>
<td headers="stub_1_65 diff_abs2019" class="gt_row gt_right">449</td>
<td headers="stub_1_65 diff_abs2021" class="gt_row gt_right">91</td>
<td headers="stub_1_65 diff_rel2019" class="gt_row gt_right">11.09%</td>
<td headers="stub_1_65 diff_rel2021" class="gt_row gt_right">2.25%</td>
<td headers="stub_1_65 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.49' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_66" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_66 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.183</td>
<td headers="stub_1_66 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autobus urbain et de banlieue, métro, tramway et train de banlieue</td>
<td headers="stub_1_66 an2010" class="gt_row gt_right">252</td>
<td headers="stub_1_66 an2019" class="gt_row gt_right">288</td>
<td headers="stub_1_66 an2021" class="gt_row gt_right">145</td>
<td headers="stub_1_66 diff_abs2019" class="gt_row gt_right">36</td>
<td headers="stub_1_66 diff_abs2021" class="gt_row gt_right">−107</td>
<td headers="stub_1_66 diff_rel2019" class="gt_row gt_right">14.29%</td>
<td headers="stub_1_66 diff_rel2021" class="gt_row gt_right">−42.46%</td>
<td headers="stub_1_66 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.63' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_67" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_67 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.184</td>
<td headers="stub_1_67 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Taxi (inclut les pourboires)</td>
<td headers="stub_1_67 an2010" class="gt_row gt_right">56</td>
<td headers="stub_1_67 an2019" class="gt_row gt_right">61</td>
<td headers="stub_1_67 an2021" class="gt_row gt_right">44</td>
<td headers="stub_1_67 diff_abs2019" class="gt_row gt_right">5</td>
<td headers="stub_1_67 diff_abs2021" class="gt_row gt_right">−12</td>
<td headers="stub_1_67 diff_rel2019" class="gt_row gt_right">8.93%</td>
<td headers="stub_1_67 diff_rel2021" class="gt_row gt_right">−21.43%</td>
<td headers="stub_1_67 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.40' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_68" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_68 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.185</td>
<td headers="stub_1_68 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres moyens de transport locaux</td>
<td headers="stub_1_68 an2010" class="gt_row gt_right">17</td>
<td headers="stub_1_68 an2019" class="gt_row gt_right">22</td>
<td headers="stub_1_68 an2021" class="gt_row gt_right">13</td>
<td headers="stub_1_68 diff_abs2019" class="gt_row gt_right">5</td>
<td headers="stub_1_68 diff_abs2021" class="gt_row gt_right">−4</td>
<td headers="stub_1_68 diff_rel2019" class="gt_row gt_right">29.41%</td>
<td headers="stub_1_68 diff_rel2021" class="gt_row gt_right">−23.53%</td>
<td headers="stub_1_68 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.30' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_69" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_69 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.186</td>
<td headers="stub_1_69 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Avion</td>
<td headers="stub_1_69 an2010" class="gt_row gt_right">309</td>
<td headers="stub_1_69 an2019" class="gt_row gt_right">482</td>
<td headers="stub_1_69 an2021" class="gt_row gt_right">132</td>
<td headers="stub_1_69 diff_abs2019" class="gt_row gt_right">173</td>
<td headers="stub_1_69 diff_abs2021" class="gt_row gt_right">−177</td>
<td headers="stub_1_69 diff_rel2019" class="gt_row gt_right">55.99%</td>
<td headers="stub_1_69 diff_rel2021" class="gt_row gt_right">−57.28%</td>
<td headers="stub_1_69 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.48' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_70" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_70 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.187</td>
<td headers="stub_1_70 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autobus interurbain</td>
<td headers="stub_1_70 an2010" class="gt_row gt_right">16</td>
<td headers="stub_1_70 an2019" class="gt_row gt_right">12</td>
<td headers="stub_1_70 an2021" class="gt_row gt_right">2</td>
<td headers="stub_1_70 diff_abs2019" class="gt_row gt_right">−4</td>
<td headers="stub_1_70 diff_abs2021" class="gt_row gt_right">−14</td>
<td headers="stub_1_70 diff_rel2019" class="gt_row gt_right">−25.00%</td>
<td headers="stub_1_70 diff_rel2021" class="gt_row gt_right">−87.50%</td>
<td headers="stub_1_70 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='8.27' y='0.89' width='1.11' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_71" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_71 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.188</td>
<td headers="stub_1_71 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres services de transport de passagers interurbain</td>
<td headers="stub_1_71 an2010" class="gt_row gt_right">20</td>
<td headers="stub_1_71 an2019" class="gt_row gt_right">28</td>
<td headers="stub_1_71 an2021" class="gt_row gt_right">7</td>
<td headers="stub_1_71 diff_abs2019" class="gt_row gt_right">8</td>
<td headers="stub_1_71 diff_abs2021" class="gt_row gt_right">−13</td>
<td headers="stub_1_71 diff_rel2019" class="gt_row gt_right">40.00%</td>
<td headers="stub_1_71 diff_rel2021" class="gt_row gt_right">−65.00%</td>
<td headers="stub_1_71 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.77' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_72" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_72 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.189</td>
<td headers="stub_1_72 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de déménagement, d'entreposage et de livraison</td>
<td headers="stub_1_72 an2010" class="gt_row gt_right">44</td>
<td headers="stub_1_72 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_72 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_72 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_72 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_72 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_72 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_72 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_73" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_73 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.342</td>
<td headers="stub_1_73 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de transport entre particuliers</td>
<td headers="stub_1_73 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_73 an2019" class="gt_row gt_right">45</td>
<td headers="stub_1_73 an2021" class="gt_row gt_right">32</td>
<td headers="stub_1_73 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_73 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_73 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_73 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_73 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_74" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_74 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.23.25.343</td>
<td headers="stub_1_74 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de déménagement et d'entreposage</td>
<td headers="stub_1_74 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_74 an2019" class="gt_row gt_right">44</td>
<td headers="stub_1_74 an2021" class="gt_row gt_right">53</td>
<td headers="stub_1_74 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_74 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_74 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_74 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_74 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_75" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_75 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.203.204</td>
<td headers="stub_1_75 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes pour les régimes privés de soins de santé</td>
<td headers="stub_1_75 an2010" class="gt_row gt_right">461</td>
<td headers="stub_1_75 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_75 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_75 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_75 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_75 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_75 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_75 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_76" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_76 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.203.205</td>
<td headers="stub_1_76 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes pour les régimes privés d'assurance-dentaire</td>
<td headers="stub_1_76 an2010" class="gt_row gt_right">40</td>
<td headers="stub_1_76 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_76 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_76 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_76 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_76 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_76 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_76 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_77" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_77 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.203.206</td>
<td headers="stub_1_77 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes pour les régimes privés d'assurance-accident ou invalidité</td>
<td headers="stub_1_77 an2010" class="gt_row gt_right">111</td>
<td headers="stub_1_77 an2019" class="gt_row gt_right">154</td>
<td headers="stub_1_77 an2021" class="gt_row gt_right">158</td>
<td headers="stub_1_77 diff_abs2019" class="gt_row gt_right">43</td>
<td headers="stub_1_77 diff_abs2021" class="gt_row gt_right">47</td>
<td headers="stub_1_77 diff_rel2019" class="gt_row gt_right">38.74%</td>
<td headers="stub_1_77 diff_rel2021" class="gt_row gt_right">42.34%</td>
<td headers="stub_1_77 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.72' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_78" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_78 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.203.346</td>
<td headers="stub_1_78 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes pour les régimes privés de soins de santé et d'assurance-dentaire</td>
<td headers="stub_1_78 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_78 an2019" class="gt_row gt_right">990</td>
<td headers="stub_1_78 an2021" class="gt_row gt_right">681</td>
<td headers="stub_1_78 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_78 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_78 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_78 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_78 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_79" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_79 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.27.191</td>
<td headers="stub_1_79 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Médicaments, produits pharmaceutiques, articles et équipement pour soins de santé sans ordonnance</td>
<td headers="stub_1_79 an2010" class="gt_row gt_right">358</td>
<td headers="stub_1_79 an2019" class="gt_row gt_right">347</td>
<td headers="stub_1_79 an2021" class="gt_row gt_right">393</td>
<td headers="stub_1_79 diff_abs2019" class="gt_row gt_right">−11</td>
<td headers="stub_1_79 diff_abs2021" class="gt_row gt_right">35</td>
<td headers="stub_1_79 diff_rel2019" class="gt_row gt_right">−3.07%</td>
<td headers="stub_1_79 diff_rel2021" class="gt_row gt_right">9.78%</td>
<td headers="stub_1_79 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.24' y='0.89' width='0.14' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_80" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_80 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.27.192</td>
<td headers="stub_1_80 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de soins de santé</td>
<td headers="stub_1_80 an2010" class="gt_row gt_right">153</td>
<td headers="stub_1_80 an2019" class="gt_row gt_right">258</td>
<td headers="stub_1_80 an2021" class="gt_row gt_right">290</td>
<td headers="stub_1_80 diff_abs2019" class="gt_row gt_right">105</td>
<td headers="stub_1_80 diff_abs2021" class="gt_row gt_right">137</td>
<td headers="stub_1_80 diff_rel2019" class="gt_row gt_right">68.63%</td>
<td headers="stub_1_80 diff_rel2021" class="gt_row gt_right">89.54%</td>
<td headers="stub_1_80 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.04' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_81" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_81 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.27.197</td>
<td headers="stub_1_81 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Articles et services pour soins des yeux</td>
<td headers="stub_1_81 an2010" class="gt_row gt_right">243</td>
<td headers="stub_1_81 an2019" class="gt_row gt_right">252</td>
<td headers="stub_1_81 an2021" class="gt_row gt_right">253</td>
<td headers="stub_1_81 diff_abs2019" class="gt_row gt_right">9</td>
<td headers="stub_1_81 diff_abs2021" class="gt_row gt_right">10</td>
<td headers="stub_1_81 diff_rel2019" class="gt_row gt_right">3.70%</td>
<td headers="stub_1_81 diff_rel2021" class="gt_row gt_right">4.12%</td>
<td headers="stub_1_81 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.16' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_82" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_82 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.27.201</td>
<td headers="stub_1_82 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Soins dentaires</td>
<td headers="stub_1_82 an2010" class="gt_row gt_right">404</td>
<td headers="stub_1_82 an2019" class="gt_row gt_right">461</td>
<td headers="stub_1_82 an2021" class="gt_row gt_right">477</td>
<td headers="stub_1_82 diff_abs2019" class="gt_row gt_right">57</td>
<td headers="stub_1_82 diff_abs2021" class="gt_row gt_right">73</td>
<td headers="stub_1_82 diff_rel2019" class="gt_row gt_right">14.11%</td>
<td headers="stub_1_82 diff_rel2021" class="gt_row gt_right">18.07%</td>
<td headers="stub_1_82 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.62' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_83" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_83 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.27.344</td>
<td headers="stub_1_83 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Médicaments et produits pharmaceutiques avec ordonnance et cannabis pour usage thérapeutique</td>
<td headers="stub_1_83 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_83 an2019" class="gt_row gt_right">502</td>
<td headers="stub_1_83 an2021" class="gt_row gt_right">644</td>
<td headers="stub_1_83 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_83 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_83 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_83 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_83 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_84" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_84 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.26.28.202</td>
<td headers="stub_1_84 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes pour les régimes d'assurance-hospitalisation et d'assurance-médicaments</td>
<td headers="stub_1_84 an2010" class="gt_row gt_right">292</td>
<td headers="stub_1_84 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_84 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_84 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_84 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_84 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_84 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_84 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_85" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_85 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.207.208</td>
<td headers="stub_1_85 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits capillaires</td>
<td headers="stub_1_85 an2010" class="gt_row gt_right">84</td>
<td headers="stub_1_85 an2019" class="gt_row gt_right">74</td>
<td headers="stub_1_85 an2021" class="gt_row gt_right">59</td>
<td headers="stub_1_85 diff_abs2019" class="gt_row gt_right">−10</td>
<td headers="stub_1_85 diff_abs2021" class="gt_row gt_right">−25</td>
<td headers="stub_1_85 diff_rel2019" class="gt_row gt_right">−11.90%</td>
<td headers="stub_1_85 diff_rel2021" class="gt_row gt_right">−29.76%</td>
<td headers="stub_1_85 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='8.85' y='0.89' width='0.53' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_86" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_86 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.207.209</td>
<td headers="stub_1_86 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Maquillage, soins de la peau, produits pour manucures et parfums</td>
<td headers="stub_1_86 an2010" class="gt_row gt_right">259</td>
<td headers="stub_1_86 an2019" class="gt_row gt_right">266</td>
<td headers="stub_1_86 an2021" class="gt_row gt_right">161</td>
<td headers="stub_1_86 diff_abs2019" class="gt_row gt_right">7</td>
<td headers="stub_1_86 diff_abs2021" class="gt_row gt_right">−98</td>
<td headers="stub_1_86 diff_rel2019" class="gt_row gt_right">2.70%</td>
<td headers="stub_1_86 diff_rel2021" class="gt_row gt_right">−37.84%</td>
<td headers="stub_1_86 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.12' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_87" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_87 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.207.212</td>
<td headers="stub_1_87 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Désodorisants personnels</td>
<td headers="stub_1_87 an2010" class="gt_row gt_right">17</td>
<td headers="stub_1_87 an2019" class="gt_row gt_right">22</td>
<td headers="stub_1_87 an2021" class="gt_row gt_right">33</td>
<td headers="stub_1_87 diff_abs2019" class="gt_row gt_right">5</td>
<td headers="stub_1_87 diff_abs2021" class="gt_row gt_right">16</td>
<td headers="stub_1_87 diff_rel2019" class="gt_row gt_right">29.41%</td>
<td headers="stub_1_87 diff_rel2021" class="gt_row gt_right">94.12%</td>
<td headers="stub_1_87 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.30' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_88" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_88 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.207.213</td>
<td headers="stub_1_88 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Savons pour le corps</td>
<td headers="stub_1_88 an2010" class="gt_row gt_right">40</td>
<td headers="stub_1_88 an2019" class="gt_row gt_right">63</td>
<td headers="stub_1_88 an2021" class="gt_row gt_right">67</td>
<td headers="stub_1_88 diff_abs2019" class="gt_row gt_right">23</td>
<td headers="stub_1_88 diff_abs2021" class="gt_row gt_right">27</td>
<td headers="stub_1_88 diff_rel2019" class="gt_row gt_right">57.50%</td>
<td headers="stub_1_88 diff_rel2021" class="gt_row gt_right">67.50%</td>
<td headers="stub_1_88 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.55' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_89" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_89 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.207.214</td>
<td headers="stub_1_89 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits d'hygiène buccale</td>
<td headers="stub_1_89 an2010" class="gt_row gt_right">59</td>
<td headers="stub_1_89 an2019" class="gt_row gt_right">58</td>
<td headers="stub_1_89 an2021" class="gt_row gt_right">85</td>
<td headers="stub_1_89 diff_abs2019" class="gt_row gt_right">−1</td>
<td headers="stub_1_89 diff_abs2021" class="gt_row gt_right">26</td>
<td headers="stub_1_89 diff_rel2019" class="gt_row gt_right">−1.69%</td>
<td headers="stub_1_89 diff_rel2021" class="gt_row gt_right">44.07%</td>
<td headers="stub_1_89 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.31' y='0.89' width='0.075' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_90" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_90 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.207.215</td>
<td headers="stub_1_90 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Couches jetables</td>
<td headers="stub_1_90 an2010" class="gt_row gt_right">64</td>
<td headers="stub_1_90 an2019" class="gt_row gt_right">33</td>
<td headers="stub_1_90 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_90 diff_abs2019" class="gt_row gt_right">−31</td>
<td headers="stub_1_90 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_90 diff_rel2019" class="gt_row gt_right">−48.44%</td>
<td headers="stub_1_90 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_90 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='7.24' y='0.89' width='2.14' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_91" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_91 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.207.216</td>
<td headers="stub_1_91 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres articles et accessoires de soins personnels</td>
<td headers="stub_1_91 an2010" class="gt_row gt_right">139</td>
<td headers="stub_1_91 an2019" class="gt_row gt_right">150</td>
<td headers="stub_1_91 an2021" class="gt_row gt_right">194</td>
<td headers="stub_1_91 diff_abs2019" class="gt_row gt_right">11</td>
<td headers="stub_1_91 diff_abs2021" class="gt_row gt_right">55</td>
<td headers="stub_1_91 diff_rel2019" class="gt_row gt_right">7.91%</td>
<td headers="stub_1_91 diff_rel2021" class="gt_row gt_right">39.57%</td>
<td headers="stub_1_91 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.35' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_92" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_92 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.217.218</td>
<td headers="stub_1_92 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de coiffure</td>
<td headers="stub_1_92 an2010" class="gt_row gt_right">231</td>
<td headers="stub_1_92 an2019" class="gt_row gt_right">415</td>
<td headers="stub_1_92 an2021" class="gt_row gt_right">533</td>
<td headers="stub_1_92 diff_abs2019" class="gt_row gt_right">184</td>
<td headers="stub_1_92 diff_abs2021" class="gt_row gt_right">302</td>
<td headers="stub_1_92 diff_rel2019" class="gt_row gt_right">79.65%</td>
<td headers="stub_1_92 diff_rel2021" class="gt_row gt_right">130.74%</td>
<td headers="stub_1_92 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.53' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_93" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_93 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.29.217.219</td>
<td headers="stub_1_93 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres services de soins personnels</td>
<td headers="stub_1_93 an2010" class="gt_row gt_right">105</td>
<td headers="stub_1_93 an2019" class="gt_row gt_right">153</td>
<td headers="stub_1_93 an2021" class="gt_row gt_right">249</td>
<td headers="stub_1_93 diff_abs2019" class="gt_row gt_right">48</td>
<td headers="stub_1_93 diff_abs2021" class="gt_row gt_right">144</td>
<td headers="stub_1_93 diff_rel2019" class="gt_row gt_right">45.71%</td>
<td headers="stub_1_93 diff_rel2021" class="gt_row gt_right">137.14%</td>
<td headers="stub_1_93 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.02' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_94" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_94 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.364</td>
<td headers="stub_1_94 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de livraison de repas prêts-à-cuisiner</td>
<td headers="stub_1_94 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_94 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_94 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_94 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_94 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_94 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_94 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_94 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_95" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_95 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4.43</td>
<td headers="stub_1_95 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits de boulangerie</td>
<td headers="stub_1_95 an2010" class="gt_row gt_right">628</td>
<td headers="stub_1_95 an2019" class="gt_row gt_right">753</td>
<td headers="stub_1_95 an2021" class="gt_row gt_right">736</td>
<td headers="stub_1_95 diff_abs2019" class="gt_row gt_right">125</td>
<td headers="stub_1_95 diff_abs2021" class="gt_row gt_right">108</td>
<td headers="stub_1_95 diff_rel2019" class="gt_row gt_right">19.90%</td>
<td headers="stub_1_95 diff_rel2021" class="gt_row gt_right">17.20%</td>
<td headers="stub_1_95 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.88' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_96" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_96 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4.44</td>
<td headers="stub_1_96 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Grains et produits céréaliers</td>
<td headers="stub_1_96 an2010" class="gt_row gt_right">283</td>
<td headers="stub_1_96 an2019" class="gt_row gt_right">375</td>
<td headers="stub_1_96 an2021" class="gt_row gt_right">413</td>
<td headers="stub_1_96 diff_abs2019" class="gt_row gt_right">92</td>
<td headers="stub_1_96 diff_abs2021" class="gt_row gt_right">130</td>
<td headers="stub_1_96 diff_rel2019" class="gt_row gt_right">32.51%</td>
<td headers="stub_1_96 diff_rel2021" class="gt_row gt_right">45.94%</td>
<td headers="stub_1_96 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.44' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_97" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_97 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4.45</td>
<td headers="stub_1_97 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Fruits, préparations à base de fruits, et noix</td>
<td headers="stub_1_97 an2010" class="gt_row gt_right">637</td>
<td headers="stub_1_97 an2019" class="gt_row gt_right">839</td>
<td headers="stub_1_97 an2021" class="gt_row gt_right">947</td>
<td headers="stub_1_97 diff_abs2019" class="gt_row gt_right">202</td>
<td headers="stub_1_97 diff_abs2021" class="gt_row gt_right">310</td>
<td headers="stub_1_97 diff_rel2019" class="gt_row gt_right">31.71%</td>
<td headers="stub_1_97 diff_rel2021" class="gt_row gt_right">48.67%</td>
<td headers="stub_1_97 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.40' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_98" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_98 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4.46</td>
<td headers="stub_1_98 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Légumes et préparations à base de légumes</td>
<td headers="stub_1_98 an2010" class="gt_row gt_right">588</td>
<td headers="stub_1_98 an2019" class="gt_row gt_right">909</td>
<td headers="stub_1_98 an2021" class="gt_row gt_right">923</td>
<td headers="stub_1_98 diff_abs2019" class="gt_row gt_right">321</td>
<td headers="stub_1_98 diff_abs2021" class="gt_row gt_right">335</td>
<td headers="stub_1_98 diff_rel2019" class="gt_row gt_right">54.59%</td>
<td headers="stub_1_98 diff_rel2021" class="gt_row gt_right">56.97%</td>
<td headers="stub_1_98 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.42' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_99" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_99 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4.47</td>
<td headers="stub_1_99 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits laitiers et oeufs</td>
<td headers="stub_1_99 an2010" class="gt_row gt_right">951</td>
<td headers="stub_1_99 an2019" class="gt_row gt_right">1,044</td>
<td headers="stub_1_99 an2021" class="gt_row gt_right">1,087</td>
<td headers="stub_1_99 diff_abs2019" class="gt_row gt_right">93</td>
<td headers="stub_1_99 diff_abs2021" class="gt_row gt_right">136</td>
<td headers="stub_1_99 diff_rel2019" class="gt_row gt_right">9.78%</td>
<td headers="stub_1_99 diff_rel2021" class="gt_row gt_right">14.30%</td>
<td headers="stub_1_99 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.43' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_100" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_100 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4.48</td>
<td headers="stub_1_100 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Viande</td>
<td headers="stub_1_100 an2010" class="gt_row gt_right">1,017</td>
<td headers="stub_1_100 an2019" class="gt_row gt_right">1,469</td>
<td headers="stub_1_100 an2021" class="gt_row gt_right">1,548</td>
<td headers="stub_1_100 diff_abs2019" class="gt_row gt_right">452</td>
<td headers="stub_1_100 diff_abs2021" class="gt_row gt_right">531</td>
<td headers="stub_1_100 diff_rel2019" class="gt_row gt_right">44.44%</td>
<td headers="stub_1_100 diff_rel2021" class="gt_row gt_right">52.21%</td>
<td headers="stub_1_100 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.97' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_101" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_101 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4.49</td>
<td headers="stub_1_101 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Poissons et fruits de mer</td>
<td headers="stub_1_101 an2010" class="gt_row gt_right">223</td>
<td headers="stub_1_101 an2019" class="gt_row gt_right">319</td>
<td headers="stub_1_101 an2021" class="gt_row gt_right">380</td>
<td headers="stub_1_101 diff_abs2019" class="gt_row gt_right">96</td>
<td headers="stub_1_101 diff_abs2021" class="gt_row gt_right">157</td>
<td headers="stub_1_101 diff_rel2019" class="gt_row gt_right">43.05%</td>
<td headers="stub_1_101 diff_rel2021" class="gt_row gt_right">70.40%</td>
<td headers="stub_1_101 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.91' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_102" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_102 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.4.50</td>
<td headers="stub_1_102 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Boissons non-alcoolisées et autres produits alimentaires</td>
<td headers="stub_1_102 an2010" class="gt_row gt_right">1,238</td>
<td headers="stub_1_102 an2019" class="gt_row gt_right">1,656</td>
<td headers="stub_1_102 an2021" class="gt_row gt_right">1,860</td>
<td headers="stub_1_102 diff_abs2019" class="gt_row gt_right">418</td>
<td headers="stub_1_102 diff_abs2021" class="gt_row gt_right">622</td>
<td headers="stub_1_102 diff_rel2019" class="gt_row gt_right">33.76%</td>
<td headers="stub_1_102 diff_rel2021" class="gt_row gt_right">50.24%</td>
<td headers="stub_1_102 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.50' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_103" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_103 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.5.51</td>
<td headers="stub_1_103 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Repas au restaurant</td>
<td headers="stub_1_103 an2010" class="gt_row gt_right">1,686</td>
<td headers="stub_1_103 an2019" class="gt_row gt_right">2,282</td>
<td headers="stub_1_103 an2021" class="gt_row gt_right">1,625</td>
<td headers="stub_1_103 diff_abs2019" class="gt_row gt_right">596</td>
<td headers="stub_1_103 diff_abs2021" class="gt_row gt_right">−61</td>
<td headers="stub_1_103 diff_rel2019" class="gt_row gt_right">35.35%</td>
<td headers="stub_1_103 diff_rel2021" class="gt_row gt_right">−3.62%</td>
<td headers="stub_1_103 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.57' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_104" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_104 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.3.5.52</td>
<td headers="stub_1_104 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Collations et breuvages au restaurant</td>
<td headers="stub_1_104 an2010" class="gt_row gt_right">158</td>
<td headers="stub_1_104 an2019" class="gt_row gt_right">200</td>
<td headers="stub_1_104 an2021" class="gt_row gt_right">149</td>
<td headers="stub_1_104 diff_abs2019" class="gt_row gt_right">42</td>
<td headers="stub_1_104 diff_abs2021" class="gt_row gt_right">−9</td>
<td headers="stub_1_104 diff_rel2019" class="gt_row gt_right">26.58%</td>
<td headers="stub_1_104 diff_rel2021" class="gt_row gt_right">−5.70%</td>
<td headers="stub_1_104 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.18' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_105" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_105 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.220</td>
<td headers="stub_1_105 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel de sport et équipement sportif et récréatif et services connexes</td>
<td headers="stub_1_105 an2010" class="gt_row gt_right">110</td>
<td headers="stub_1_105 an2019" class="gt_row gt_right">231</td>
<td headers="stub_1_105 an2021" class="gt_row gt_right">220</td>
<td headers="stub_1_105 diff_abs2019" class="gt_row gt_right">121</td>
<td headers="stub_1_105 diff_abs2021" class="gt_row gt_right">110</td>
<td headers="stub_1_105 diff_rel2019" class="gt_row gt_right">110.00%</td>
<td headers="stub_1_105 diff_rel2021" class="gt_row gt_right">100.00%</td>
<td headers="stub_1_105 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='4.87' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_106" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_106 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.221</td>
<td headers="stub_1_106 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Équipement de jeux extérieurs et accessoires</td>
<td headers="stub_1_106 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_106 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_106 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_106 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_106 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_106 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_106 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_106 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_107" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_107 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.222</td>
<td headers="stub_1_107 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Jouets pour enfants</td>
<td headers="stub_1_107 an2010" class="gt_row gt_right">96</td>
<td headers="stub_1_107 an2019" class="gt_row gt_right">113</td>
<td headers="stub_1_107 an2021" class="gt_row gt_right">137</td>
<td headers="stub_1_107 diff_abs2019" class="gt_row gt_right">17</td>
<td headers="stub_1_107 diff_abs2021" class="gt_row gt_right">41</td>
<td headers="stub_1_107 diff_rel2019" class="gt_row gt_right">17.71%</td>
<td headers="stub_1_107 diff_rel2021" class="gt_row gt_right">42.71%</td>
<td headers="stub_1_107 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.78' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_108" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_108 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.223</td>
<td headers="stub_1_108 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Console de jeux vidéo et accessoires (sauf pour les ordinateurs)</td>
<td headers="stub_1_108 an2010" class="gt_row gt_right">93</td>
<td headers="stub_1_108 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_108 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_108 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_108 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_108 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_108 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_108 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_109" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_109 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.224</td>
<td headers="stub_1_109 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel d'art et d'artisanat</td>
<td headers="stub_1_109 an2010" class="gt_row gt_right">9</td>
<td headers="stub_1_109 an2019" class="gt_row gt_right">24</td>
<td headers="stub_1_109 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_109 diff_abs2019" class="gt_row gt_right">15</td>
<td headers="stub_1_109 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_109 diff_rel2019" class="gt_row gt_right">166.67%</td>
<td headers="stub_1_109 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_109 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='7.38' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_110" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_110 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.225</td>
<td headers="stub_1_110 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel informatique et fournitures</td>
<td headers="stub_1_110 an2010" class="gt_row gt_right">321</td>
<td headers="stub_1_110 an2019" class="gt_row gt_right">297</td>
<td headers="stub_1_110 an2021" class="gt_row gt_right">654</td>
<td headers="stub_1_110 diff_abs2019" class="gt_row gt_right">−24</td>
<td headers="stub_1_110 diff_abs2021" class="gt_row gt_right">333</td>
<td headers="stub_1_110 diff_rel2019" class="gt_row gt_right">−7.48%</td>
<td headers="stub_1_110 diff_rel2021" class="gt_row gt_right">103.74%</td>
<td headers="stub_1_110 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.05' y='0.89' width='0.33' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_111" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_111 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.229</td>
<td headers="stub_1_111 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel et services photographiques</td>
<td headers="stub_1_111 an2010" class="gt_row gt_right">121</td>
<td headers="stub_1_111 an2019" class="gt_row gt_right">53</td>
<td headers="stub_1_111 an2021" class="gt_row gt_right">83</td>
<td headers="stub_1_111 diff_abs2019" class="gt_row gt_right">−68</td>
<td headers="stub_1_111 diff_abs2021" class="gt_row gt_right">−38</td>
<td headers="stub_1_111 diff_rel2019" class="gt_row gt_right">−56.20%</td>
<td headers="stub_1_111 diff_rel2021" class="gt_row gt_right">−31.40%</td>
<td headers="stub_1_111 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='6.89' y='0.89' width='2.49' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_112" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_112 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.232</td>
<td headers="stub_1_112 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Articles de collectionneurs (e.g. timbres, pièces de monnaie)</td>
<td headers="stub_1_112 an2010" class="gt_row gt_right">8</td>
<td headers="stub_1_112 an2019" class="gt_row gt_right">19</td>
<td headers="stub_1_112 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_112 diff_abs2019" class="gt_row gt_right">11</td>
<td headers="stub_1_112 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_112 diff_rel2019" class="gt_row gt_right">137.50%</td>
<td headers="stub_1_112 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_112 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='6.09' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_113" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_113 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.233</td>
<td headers="stub_1_113 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autre équipement pour les activités récréatives et les services connexes</td>
<td headers="stub_1_113 an2010" class="gt_row gt_right">70</td>
<td headers="stub_1_113 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_113 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_113 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_113 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_113 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_113 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_113 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_114" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_114 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.31.348</td>
<td headers="stub_1_114 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autre équipement pour les activités récréatives</td>
<td headers="stub_1_114 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_114 an2019" class="gt_row gt_right">49</td>
<td headers="stub_1_114 an2021" class="gt_row gt_right">91</td>
<td headers="stub_1_114 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_114 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_114 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_114 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_114 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_115" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_115 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.32.234</td>
<td headers="stub_1_115 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Matériel de divertissement au foyer</td>
<td headers="stub_1_115 an2010" class="gt_row gt_right">402</td>
<td headers="stub_1_115 an2019" class="gt_row gt_right">146</td>
<td headers="stub_1_115 an2021" class="gt_row gt_right">304</td>
<td headers="stub_1_115 diff_abs2019" class="gt_row gt_right">−256</td>
<td headers="stub_1_115 diff_abs2021" class="gt_row gt_right">−98</td>
<td headers="stub_1_115 diff_rel2019" class="gt_row gt_right">−63.68%</td>
<td headers="stub_1_115 diff_rel2021" class="gt_row gt_right">−24.38%</td>
<td headers="stub_1_115 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='6.56' y='0.89' width='2.82' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_116" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_116 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.32.242</td>
<td headers="stub_1_116 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services de divertissement au foyer</td>
<td headers="stub_1_116 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_116 an2019" class="gt_row gt_right">18</td>
<td headers="stub_1_116 an2021" class="gt_row gt_right">34</td>
<td headers="stub_1_116 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_116 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_116 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_116 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_116 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_117" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_117 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.33.245</td>
<td headers="stub_1_117 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Divertissement</td>
<td headers="stub_1_117 an2010" class="gt_row gt_right">671</td>
<td headers="stub_1_117 an2019" class="gt_row gt_right">808</td>
<td headers="stub_1_117 an2021" class="gt_row gt_right">668</td>
<td headers="stub_1_117 diff_abs2019" class="gt_row gt_right">137</td>
<td headers="stub_1_117 diff_abs2021" class="gt_row gt_right">−3</td>
<td headers="stub_1_117 diff_rel2019" class="gt_row gt_right">20.42%</td>
<td headers="stub_1_117 diff_rel2021" class="gt_row gt_right">−0.45%</td>
<td headers="stub_1_117 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.90' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_118" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_118 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.33.252</td>
<td headers="stub_1_118 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Fréquentation d'établissements récréatifs</td>
<td headers="stub_1_118 an2010" class="gt_row gt_right">190</td>
<td headers="stub_1_118 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_118 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_118 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_118 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_118 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_118 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_118 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_119" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_119 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.33.255</td>
<td headers="stub_1_119 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Forfait-voyages</td>
<td headers="stub_1_119 an2010" class="gt_row gt_right">456</td>
<td headers="stub_1_119 an2019" class="gt_row gt_right">804</td>
<td headers="stub_1_119 an2021" class="gt_row gt_right">167</td>
<td headers="stub_1_119 diff_abs2019" class="gt_row gt_right">348</td>
<td headers="stub_1_119 diff_abs2021" class="gt_row gt_right">−289</td>
<td headers="stub_1_119 diff_rel2019" class="gt_row gt_right">76.32%</td>
<td headers="stub_1_119 diff_rel2021" class="gt_row gt_right">−63.38%</td>
<td headers="stub_1_119 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.38' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_120" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_120 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.33.256</td>
<td headers="stub_1_120 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres activités et services récréatifs</td>
<td headers="stub_1_120 an2010" class="gt_row gt_right">41</td>
<td headers="stub_1_120 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_120 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_120 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_120 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_120 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_120 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_120 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_121" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_121 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.33.354</td>
<td headers="stub_1_121 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Fréquentation d'établissements récréatifs et frais pour autres activités récréatives</td>
<td headers="stub_1_121 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_121 an2019" class="gt_row gt_right">467</td>
<td headers="stub_1_121 an2021" class="gt_row gt_right">249</td>
<td headers="stub_1_121 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_121 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_121 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_121 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_121 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_122" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_122 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.33.357</td>
<td headers="stub_1_122 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres services récréatifs</td>
<td headers="stub_1_122 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_122 an2019" class="gt_row gt_right">47</td>
<td headers="stub_1_122 an2021" class="gt_row gt_right">47</td>
<td headers="stub_1_122 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_122 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_122 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_122 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_122 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_123" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_123 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.34.257</td>
<td headers="stub_1_123 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Achat de véhicules récréatifs</td>
<td headers="stub_1_123 an2010" class="gt_row gt_right">413</td>
<td headers="stub_1_123 an2019" class="gt_row gt_right">431</td>
<td headers="stub_1_123 an2021" class="gt_row gt_right">813</td>
<td headers="stub_1_123 diff_abs2019" class="gt_row gt_right">18</td>
<td headers="stub_1_123 diff_abs2021" class="gt_row gt_right">400</td>
<td headers="stub_1_123 diff_rel2019" class="gt_row gt_right">4.36%</td>
<td headers="stub_1_123 diff_rel2021" class="gt_row gt_right">96.85%</td>
<td headers="stub_1_123 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.19' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_124" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_124 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.30.34.262</td>
<td headers="stub_1_124 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Utilisation de véhicules récréatifs</td>
<td headers="stub_1_124 an2010" class="gt_row gt_right">124</td>
<td headers="stub_1_124 an2019" class="gt_row gt_right">185</td>
<td headers="stub_1_124 an2021" class="gt_row gt_right">306</td>
<td headers="stub_1_124 diff_abs2019" class="gt_row gt_right">61</td>
<td headers="stub_1_124 diff_abs2021" class="gt_row gt_right">182</td>
<td headers="stub_1_124 diff_rel2019" class="gt_row gt_right">49.19%</td>
<td headers="stub_1_124 diff_rel2021" class="gt_row gt_right">146.77%</td>
<td headers="stub_1_124 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.18' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_125" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_125 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35.267.268</td>
<td headers="stub_1_125 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de scolarité pour la maternelle, l'école élémentaire et le secondaire</td>
<td headers="stub_1_125 an2010" class="gt_row gt_right">162</td>
<td headers="stub_1_125 an2019" class="gt_row gt_right">201</td>
<td headers="stub_1_125 an2021" class="gt_row gt_right">270</td>
<td headers="stub_1_125 diff_abs2019" class="gt_row gt_right">39</td>
<td headers="stub_1_125 diff_abs2021" class="gt_row gt_right">108</td>
<td headers="stub_1_125 diff_rel2019" class="gt_row gt_right">24.07%</td>
<td headers="stub_1_125 diff_rel2021" class="gt_row gt_right">66.67%</td>
<td headers="stub_1_125 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.07' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_126" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_126 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35.267.269</td>
<td headers="stub_1_126 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de scolarité pour les études universitaires</td>
<td headers="stub_1_126 an2010" class="gt_row gt_right">252</td>
<td headers="stub_1_126 an2019" class="gt_row gt_right">331</td>
<td headers="stub_1_126 an2021" class="gt_row gt_right">381</td>
<td headers="stub_1_126 diff_abs2019" class="gt_row gt_right">79</td>
<td headers="stub_1_126 diff_abs2021" class="gt_row gt_right">129</td>
<td headers="stub_1_126 diff_rel2019" class="gt_row gt_right">31.35%</td>
<td headers="stub_1_126 diff_rel2021" class="gt_row gt_right">51.19%</td>
<td headers="stub_1_126 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.39' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_127" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_127 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35.267.270</td>
<td headers="stub_1_127 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de scolarité pour formations autres (collège, écoles de métiers et instituts de formation professionnelle)</td>
<td headers="stub_1_127 an2010" class="gt_row gt_right">105</td>
<td headers="stub_1_127 an2019" class="gt_row gt_right">83</td>
<td headers="stub_1_127 an2021" class="gt_row gt_right">132</td>
<td headers="stub_1_127 diff_abs2019" class="gt_row gt_right">−22</td>
<td headers="stub_1_127 diff_abs2021" class="gt_row gt_right">27</td>
<td headers="stub_1_127 diff_rel2019" class="gt_row gt_right">−20.95%</td>
<td headers="stub_1_127 diff_rel2021" class="gt_row gt_right">25.71%</td>
<td headers="stub_1_127 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='8.45' y='0.89' width='0.93' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_128" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_128 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35.267.271</td>
<td headers="stub_1_128 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres services éducatifs</td>
<td headers="stub_1_128 an2010" class="gt_row gt_right">6</td>
<td headers="stub_1_128 an2019" class="gt_row gt_right">63</td>
<td headers="stub_1_128 an2021" class="gt_row gt_right">19</td>
<td headers="stub_1_128 diff_abs2019" class="gt_row gt_right">57</td>
<td headers="stub_1_128 diff_abs2021" class="gt_row gt_right">13</td>
<td headers="stub_1_128 diff_rel2019" class="gt_row gt_right">950.00%</td>
<td headers="stub_1_128 diff_rel2021" class="gt_row gt_right">216.67%</td>
<td headers="stub_1_128 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='42.07' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_129" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_129 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35.267.272</td>
<td headers="stub_1_129 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cours et leçons d’intérêt personnel (sauf les cours de conduite)</td>
<td headers="stub_1_129 an2010" class="gt_row gt_right">93</td>
<td headers="stub_1_129 an2019" class="gt_row gt_right">108</td>
<td headers="stub_1_129 an2021" class="gt_row gt_right">97</td>
<td headers="stub_1_129 diff_abs2019" class="gt_row gt_right">15</td>
<td headers="stub_1_129 diff_abs2021" class="gt_row gt_right">4</td>
<td headers="stub_1_129 diff_rel2019" class="gt_row gt_right">16.13%</td>
<td headers="stub_1_129 diff_rel2021" class="gt_row gt_right">4.30%</td>
<td headers="stub_1_129 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.71' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_130" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_130 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.35.273</td>
<td headers="stub_1_130 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Manuels et fournitures scolaires</td>
<td headers="stub_1_130 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_130 an2019" class="gt_row gt_right">150</td>
<td headers="stub_1_130 an2021" class="gt_row gt_right">143</td>
<td headers="stub_1_130 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_130 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_130 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_130 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_130 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_131" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_131 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.359</td>
<td headers="stub_1_131 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Produits de tabac, boissons alcoolisées et cannabis pour usage non-thérapeutique</td>
<td headers="stub_1_131 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_131 an2019" class="gt_row gt_right">1,894</td>
<td headers="stub_1_131 an2021" class="gt_row gt_right">1,859</td>
<td headers="stub_1_131 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_131 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_131 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_131 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_131 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_132" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_132 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.274</td>
<td headers="stub_1_132 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Journaux</td>
<td headers="stub_1_132 an2010" class="gt_row gt_right">43</td>
<td headers="stub_1_132 an2019" class="gt_row gt_right">10</td>
<td headers="stub_1_132 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_132 diff_abs2019" class="gt_row gt_right">−33</td>
<td headers="stub_1_132 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_132 diff_rel2019" class="gt_row gt_right">−76.74%</td>
<td headers="stub_1_132 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_132 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.98' y='0.89' width='3.40' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_133" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_133 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.275</td>
<td headers="stub_1_133 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Revues et publications périodiques</td>
<td headers="stub_1_133 an2010" class="gt_row gt_right">32</td>
<td headers="stub_1_133 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_133 an2021" class="gt_row gt_right">7</td>
<td headers="stub_1_133 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_133 diff_abs2021" class="gt_row gt_right">−25</td>
<td headers="stub_1_133 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_133 diff_rel2021" class="gt_row gt_right">−78.12%</td>
<td headers="stub_1_133 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_134" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_134 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.276</td>
<td headers="stub_1_134 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Livres et livres numériques (sauf les manuels scolaires)</td>
<td headers="stub_1_134 an2010" class="gt_row gt_right">92</td>
<td headers="stub_1_134 an2019" class="gt_row gt_right">84</td>
<td headers="stub_1_134 an2021" class="gt_row gt_right">102</td>
<td headers="stub_1_134 diff_abs2019" class="gt_row gt_right">−8</td>
<td headers="stub_1_134 diff_abs2021" class="gt_row gt_right">10</td>
<td headers="stub_1_134 diff_rel2019" class="gt_row gt_right">−8.70%</td>
<td headers="stub_1_134 diff_rel2021" class="gt_row gt_right">10.87%</td>
<td headers="stub_1_134 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.00' y='0.89' width='0.39' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_135" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_135 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.277</td>
<td headers="stub_1_135 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cartes géographiques, partitions de musique et autres produits imprimés</td>
<td headers="stub_1_135 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_135 an2019" class="gt_row gt_right">7</td>
<td headers="stub_1_135 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_135 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_135 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_135 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_135 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_135 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_136" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_136 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.36.278</td>
<td headers="stub_1_136 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services reliés au matériel de lecture (e.g. reproduction, frais de bibliothèque)</td>
<td headers="stub_1_136 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_136 an2019" class="gt_row gt_right">14</td>
<td headers="stub_1_136 an2021" class="gt_row gt_right">17</td>
<td headers="stub_1_136 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_136 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_136 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_136 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_136 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_137" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_137 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.279.280</td>
<td headers="stub_1_137 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cigarettes</td>
<td headers="stub_1_137 an2010" class="gt_row gt_right">289</td>
<td headers="stub_1_137 an2019" class="gt_row gt_right">497</td>
<td headers="stub_1_137 an2021" class="gt_row gt_right">533</td>
<td headers="stub_1_137 diff_abs2019" class="gt_row gt_right">208</td>
<td headers="stub_1_137 diff_abs2021" class="gt_row gt_right">244</td>
<td headers="stub_1_137 diff_rel2019" class="gt_row gt_right">71.97%</td>
<td headers="stub_1_137 diff_rel2021" class="gt_row gt_right">84.43%</td>
<td headers="stub_1_137 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.19' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_138" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_138 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.279.281</td>
<td headers="stub_1_138 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres produits de tabac et articles pour fumeurs</td>
<td headers="stub_1_138 an2010" class="gt_row gt_right">7</td>
<td headers="stub_1_138 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_138 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_138 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_138 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_138 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_138 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_138 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_139" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_139 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.279.360</td>
<td headers="stub_1_139 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres produits de tabac, articles pour fumeurs et cigarettes électroniques</td>
<td headers="stub_1_139 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_139 an2019" class="gt_row gt_right">33</td>
<td headers="stub_1_139 an2021" class="gt_row gt_right">76</td>
<td headers="stub_1_139 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_139 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_139 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_139 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_139 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_140" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_140 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.282.283</td>
<td headers="stub_1_140 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Boissons alcoolisées servies dans des établissements licenciés et dans les restaurants</td>
<td headers="stub_1_140 an2010" class="gt_row gt_right">171</td>
<td headers="stub_1_140 an2019" class="gt_row gt_right">311</td>
<td headers="stub_1_140 an2021" class="gt_row gt_right">251</td>
<td headers="stub_1_140 diff_abs2019" class="gt_row gt_right">140</td>
<td headers="stub_1_140 diff_abs2021" class="gt_row gt_right">80</td>
<td headers="stub_1_140 diff_rel2019" class="gt_row gt_right">81.87%</td>
<td headers="stub_1_140 diff_rel2021" class="gt_row gt_right">46.78%</td>
<td headers="stub_1_140 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.63' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_141" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_141 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.282.284</td>
<td headers="stub_1_141 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Boissons alcoolisées achetées au magasin</td>
<td headers="stub_1_141 an2010" class="gt_row gt_right">951</td>
<td headers="stub_1_141 an2019" class="gt_row gt_right">985</td>
<td headers="stub_1_141 an2021" class="gt_row gt_right">909</td>
<td headers="stub_1_141 diff_abs2019" class="gt_row gt_right">34</td>
<td headers="stub_1_141 diff_abs2021" class="gt_row gt_right">−42</td>
<td headers="stub_1_141 diff_rel2019" class="gt_row gt_right">3.58%</td>
<td headers="stub_1_141 diff_rel2021" class="gt_row gt_right">−4.42%</td>
<td headers="stub_1_141 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.16' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_142" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_142 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.282.285</td>
<td headers="stub_1_142 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Boissons alcoolisées produites par le ménage</td>
<td headers="stub_1_142 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_142 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_142 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_142 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_142 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_142 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_142 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_142 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_143" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_143 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.37.361</td>
<td headers="stub_1_143 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cannabis pour usage non-thérapeutique</td>
<td headers="stub_1_143 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_143 an2019" class="gt_row gt_right">67</td>
<td headers="stub_1_143 an2021" class="gt_row gt_right">90</td>
<td headers="stub_1_143 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_143 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_143 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_143 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_143 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_144" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_144 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.38.286</td>
<td headers="stub_1_144 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Billets de loteries sous administration publique</td>
<td headers="stub_1_144 an2010" class="gt_row gt_right">130</td>
<td headers="stub_1_144 an2019" class="gt_row gt_right">149</td>
<td headers="stub_1_144 an2021" class="gt_row gt_right">136</td>
<td headers="stub_1_144 diff_abs2019" class="gt_row gt_right">19</td>
<td headers="stub_1_144 diff_abs2021" class="gt_row gt_right">6</td>
<td headers="stub_1_144 diff_rel2019" class="gt_row gt_right">14.62%</td>
<td headers="stub_1_144 diff_rel2021" class="gt_row gt_right">4.62%</td>
<td headers="stub_1_144 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.65' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_145" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_145 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.38.287.288</td>
<td headers="stub_1_145 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Casinos, bingos et machines de jeux de hasard</td>
<td headers="stub_1_145 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_145 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_145 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_145 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_145 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_145 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_145 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_145 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_146" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_146 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.38.287.289</td>
<td headers="stub_1_146 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Billets de loterie et tirages non organisés par les administrations publiques</td>
<td headers="stub_1_146 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_146 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_146 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_146 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_146 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_146 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_146 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_146 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_147" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_147 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.290.291</td>
<td headers="stub_1_147 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de services bancaires et d'autres institutions financières</td>
<td headers="stub_1_147 an2010" class="gt_row gt_right">105</td>
<td headers="stub_1_147 an2019" class="gt_row gt_right">231</td>
<td headers="stub_1_147 an2021" class="gt_row gt_right">123</td>
<td headers="stub_1_147 diff_abs2019" class="gt_row gt_right">126</td>
<td headers="stub_1_147 diff_abs2021" class="gt_row gt_right">18</td>
<td headers="stub_1_147 diff_rel2019" class="gt_row gt_right">120.00%</td>
<td headers="stub_1_147 diff_rel2021" class="gt_row gt_right">17.14%</td>
<td headers="stub_1_147 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='5.31' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_148" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_148 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.290.292</td>
<td headers="stub_1_148 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Commissions pour des actions et obligations</td>
<td headers="stub_1_148 an2010" class="gt_row gt_right">29</td>
<td headers="stub_1_148 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_148 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_148 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_148 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_148 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_148 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_148 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_149" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_149 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.290.293</td>
<td headers="stub_1_149 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de courtage et autres services semblables</td>
<td headers="stub_1_149 an2010" class="gt_row gt_right">43</td>
<td headers="stub_1_149 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_149 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_149 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_149 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_149 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_149 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_149 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_150" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_150 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.290.294</td>
<td headers="stub_1_150 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres services financiers</td>
<td headers="stub_1_150 an2010" class="gt_row gt_right">89</td>
<td headers="stub_1_150 an2019" class="gt_row gt_right">138</td>
<td headers="stub_1_150 an2021" class="gt_row gt_right">139</td>
<td headers="stub_1_150 diff_abs2019" class="gt_row gt_right">49</td>
<td headers="stub_1_150 diff_abs2021" class="gt_row gt_right">50</td>
<td headers="stub_1_150 diff_rel2019" class="gt_row gt_right">55.06%</td>
<td headers="stub_1_150 diff_rel2021" class="gt_row gt_right">56.18%</td>
<td headers="stub_1_150 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.44' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_151" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_151 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.290.362</td>
<td headers="stub_1_151 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de courtage et commissions pour des actions et obligations</td>
<td headers="stub_1_151 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_151 an2019" class="gt_row gt_right">119</td>
<td headers="stub_1_151 an2021" class="gt_row gt_right">205</td>
<td headers="stub_1_151 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_151 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_151 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_151 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_151 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_152" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_152 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.296</td>
<td headers="stub_1_152 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dépôts perdus par défaut, amendes et argent perdu ou volé</td>
<td headers="stub_1_152 an2010" class="gt_row gt_right">81</td>
<td headers="stub_1_152 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_152 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_152 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_152 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_152 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_152 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_152 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_153" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_153 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.297</td>
<td headers="stub_1_153 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Honoraires d'avocat et de notaire non reliés au logement</td>
<td headers="stub_1_153 an2010" class="gt_row gt_right">96</td>
<td headers="stub_1_153 an2019" class="gt_row gt_right">176</td>
<td headers="stub_1_153 an2021" class="gt_row gt_right">159</td>
<td headers="stub_1_153 diff_abs2019" class="gt_row gt_right">80</td>
<td headers="stub_1_153 diff_abs2021" class="gt_row gt_right">63</td>
<td headers="stub_1_153 diff_rel2019" class="gt_row gt_right">83.33%</td>
<td headers="stub_1_153 diff_rel2021" class="gt_row gt_right">65.62%</td>
<td headers="stub_1_153 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.69' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_154" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_154 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.298</td>
<td headers="stub_1_154 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cotisations syndicales et professionnelles</td>
<td headers="stub_1_154 an2010" class="gt_row gt_right">296</td>
<td headers="stub_1_154 an2019" class="gt_row gt_right">322</td>
<td headers="stub_1_154 an2021" class="gt_row gt_right">365</td>
<td headers="stub_1_154 diff_abs2019" class="gt_row gt_right">26</td>
<td headers="stub_1_154 diff_abs2021" class="gt_row gt_right">69</td>
<td headers="stub_1_154 diff_rel2019" class="gt_row gt_right">8.78%</td>
<td headers="stub_1_154 diff_rel2021" class="gt_row gt_right">23.31%</td>
<td headers="stub_1_154 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.39' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_155" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_155 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.299</td>
<td headers="stub_1_155 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Contributions et cotisations à des clubs sociaux et d'autres organisations</td>
<td headers="stub_1_155 an2010" class="gt_row gt_right">31</td>
<td headers="stub_1_155 an2019" class="gt_row gt_right">40</td>
<td headers="stub_1_155 an2021" class="gt_row gt_right">30</td>
<td headers="stub_1_155 diff_abs2019" class="gt_row gt_right">9</td>
<td headers="stub_1_155 diff_abs2021" class="gt_row gt_right">−1</td>
<td headers="stub_1_155 diff_rel2019" class="gt_row gt_right">29.03%</td>
<td headers="stub_1_155 diff_rel2021" class="gt_row gt_right">−3.23%</td>
<td headers="stub_1_155 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.29' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_156" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_156 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.300</td>
<td headers="stub_1_156 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services funéraires</td>
<td headers="stub_1_156 an2010" class="gt_row gt_right">79</td>
<td headers="stub_1_156 an2019" class="gt_row gt_right">141</td>
<td headers="stub_1_156 an2021" class="gt_row gt_right">142</td>
<td headers="stub_1_156 diff_abs2019" class="gt_row gt_right">62</td>
<td headers="stub_1_156 diff_abs2021" class="gt_row gt_right">63</td>
<td headers="stub_1_156 diff_rel2019" class="gt_row gt_right">78.48%</td>
<td headers="stub_1_156 diff_rel2021" class="gt_row gt_right">79.75%</td>
<td headers="stub_1_156 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.48' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_157" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_157 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.301</td>
<td headers="stub_1_157 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Services gouvernementaux</td>
<td headers="stub_1_157 an2010" class="gt_row gt_right">35</td>
<td headers="stub_1_157 an2019" class="gt_row gt_right">84</td>
<td headers="stub_1_157 an2021" class="gt_row gt_right">30</td>
<td headers="stub_1_157 diff_abs2019" class="gt_row gt_right">49</td>
<td headers="stub_1_157 diff_abs2021" class="gt_row gt_right">−5</td>
<td headers="stub_1_157 diff_rel2019" class="gt_row gt_right">140.00%</td>
<td headers="stub_1_157 diff_rel2021" class="gt_row gt_right">−14.29%</td>
<td headers="stub_1_157 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='6.20' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_158" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_158 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.302</td>
<td headers="stub_1_158 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Adhésion aux magasins de gros/magasins de détails</td>
<td headers="stub_1_158 an2010" class="gt_row gt_right">18</td>
<td headers="stub_1_158 an2019" class="gt_row gt_right">45</td>
<td headers="stub_1_158 an2021" class="gt_row gt_right">75</td>
<td headers="stub_1_158 diff_abs2019" class="gt_row gt_right">27</td>
<td headers="stub_1_158 diff_abs2021" class="gt_row gt_right">57</td>
<td headers="stub_1_158 diff_rel2019" class="gt_row gt_right">150.00%</td>
<td headers="stub_1_158 diff_rel2021" class="gt_row gt_right">316.67%</td>
<td headers="stub_1_158 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='6.64' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_159" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_159 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.303</td>
<td headers="stub_1_159 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres biens et services</td>
<td headers="stub_1_159 an2010" class="gt_row gt_right">155</td>
<td headers="stub_1_159 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_159 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_159 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_159 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_159 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_159 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_159 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_160" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_160 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.304</td>
<td headers="stub_1_160 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Rabais et remboursements</td>
<td headers="stub_1_160 an2010" class="gt_row gt_right">−69</td>
<td headers="stub_1_160 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_160 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_160 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_160 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_160 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_160 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_160 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_161" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_161 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.305</td>
<td headers="stub_1_161 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de recyclage et autres frais environnementaux</td>
<td headers="stub_1_161 an2010" class="gt_row gt_right">7</td>
<td headers="stub_1_161 an2019" class="gt_row gt_right">10</td>
<td headers="stub_1_161 an2021" class="gt_row gt_right">7</td>
<td headers="stub_1_161 diff_abs2019" class="gt_row gt_right">3</td>
<td headers="stub_1_161 diff_abs2021" class="gt_row gt_right">0</td>
<td headers="stub_1_161 diff_rel2019" class="gt_row gt_right">42.86%</td>
<td headers="stub_1_161 diff_rel2021" class="gt_row gt_right">0.00%</td>
<td headers="stub_1_161 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.90' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_162" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_162 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.306</td>
<td headers="stub_1_162 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres dépenses générales</td>
<td headers="stub_1_162 an2010" class="gt_row gt_right">59</td>
<td headers="stub_1_162 an2019" class="gt_row gt_right">2</td>
<td headers="stub_1_162 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_162 diff_abs2019" class="gt_row gt_right">−57</td>
<td headers="stub_1_162 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_162 diff_rel2019" class="gt_row gt_right">−96.61%</td>
<td headers="stub_1_162 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_162 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='5.10' y='0.89' width='4.28' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_163" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_163 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.363</td>
<td headers="stub_1_163 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Contraventions</td>
<td headers="stub_1_163 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_163 an2019" class="gt_row gt_right">83</td>
<td headers="stub_1_163 an2021" class="gt_row gt_right">63</td>
<td headers="stub_1_163 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_163 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_163 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_163 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_163 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_164" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_164 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.39.295.367</td>
<td headers="stub_1_164 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Frais de commodité</td>
<td headers="stub_1_164 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_164 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_164 an2021" class="gt_row gt_right">4</td>
<td headers="stub_1_164 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_164 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_164 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_164 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_164 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_165" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_165 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6.11.73</td>
<td headers="stub_1_165 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Résidences secondaires appartenant au ménage</td>
<td headers="stub_1_165 an2010" class="gt_row gt_right">340</td>
<td headers="stub_1_165 an2019" class="gt_row gt_right">456</td>
<td headers="stub_1_165 an2021" class="gt_row gt_right">397</td>
<td headers="stub_1_165 diff_abs2019" class="gt_row gt_right">116</td>
<td headers="stub_1_165 diff_abs2021" class="gt_row gt_right">57</td>
<td headers="stub_1_165 diff_rel2019" class="gt_row gt_right">34.12%</td>
<td headers="stub_1_165 diff_rel2021" class="gt_row gt_right">16.76%</td>
<td headers="stub_1_165 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.51' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_166" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_166 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6.11.79</td>
<td headers="stub_1_166 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Autres propriétés appartenant au ménage</td>
<td headers="stub_1_166 an2010" class="gt_row gt_right">-</td>
<td headers="stub_1_166 an2019" class="gt_row gt_right">310</td>
<td headers="stub_1_166 an2021" class="gt_row gt_right">355</td>
<td headers="stub_1_166 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_166 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_166 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_166 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_166 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_167" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_167 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6.11.80</td>
<td headers="stub_1_167 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Hébergement hors du foyer</td>
<td headers="stub_1_167 an2010" class="gt_row gt_right">328</td>
<td headers="stub_1_167 an2019" class="gt_row gt_right">600</td>
<td headers="stub_1_167 an2021" class="gt_row gt_right">360</td>
<td headers="stub_1_167 diff_abs2019" class="gt_row gt_right">272</td>
<td headers="stub_1_167 diff_abs2021" class="gt_row gt_right">32</td>
<td headers="stub_1_167 diff_rel2019" class="gt_row gt_right">82.93%</td>
<td headers="stub_1_167 diff_rel2021" class="gt_row gt_right">9.76%</td>
<td headers="stub_1_167 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.67' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_168" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_168 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6.7.10</td>
<td headers="stub_1_168 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Eau, combustibles et électricité pour le logement principal</td>
<td headers="stub_1_168 an2010" class="gt_row gt_right">1,626</td>
<td headers="stub_1_168 an2019" class="gt_row gt_right">1,838</td>
<td headers="stub_1_168 an2021" class="gt_row gt_right">1,895</td>
<td headers="stub_1_168 diff_abs2019" class="gt_row gt_right">212</td>
<td headers="stub_1_168 diff_abs2021" class="gt_row gt_right">269</td>
<td headers="stub_1_168 diff_rel2019" class="gt_row gt_right">13.04%</td>
<td headers="stub_1_168 diff_rel2021" class="gt_row gt_right">16.54%</td>
<td headers="stub_1_168 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.58' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_169" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_169 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6.7.8</td>
<td headers="stub_1_169 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Logement loué par l'occupant</td>
<td headers="stub_1_169 an2010" class="gt_row gt_right">3,234</td>
<td headers="stub_1_169 an2019" class="gt_row gt_right">3,866</td>
<td headers="stub_1_169 an2021" class="gt_row gt_right">3,898</td>
<td headers="stub_1_169 diff_abs2019" class="gt_row gt_right">632</td>
<td headers="stub_1_169 diff_abs2021" class="gt_row gt_right">664</td>
<td headers="stub_1_169 diff_rel2019" class="gt_row gt_right">19.54%</td>
<td headers="stub_1_169 diff_rel2021" class="gt_row gt_right">20.53%</td>
<td headers="stub_1_169 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.87' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_170" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_170 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.2.6.7.9</td>
<td headers="stub_1_170 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Logement appartenant à l'occupant</td>
<td headers="stub_1_170 an2010" class="gt_row gt_right">6,297</td>
<td headers="stub_1_170 an2019" class="gt_row gt_right">8,751</td>
<td headers="stub_1_170 an2021" class="gt_row gt_right">8,976</td>
<td headers="stub_1_170 diff_abs2019" class="gt_row gt_right">2,454</td>
<td headers="stub_1_170 diff_abs2021" class="gt_row gt_right">2,679</td>
<td headers="stub_1_170 diff_rel2019" class="gt_row gt_right">38.97%</td>
<td headers="stub_1_170 diff_rel2021" class="gt_row gt_right">42.54%</td>
<td headers="stub_1_170 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='1.73' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_171" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_171 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.40</td>
<td headers="stub_1_171 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Impôts sur le revenu</td>
<td headers="stub_1_171 an2010" class="gt_row gt_right">10,130</td>
<td headers="stub_1_171 an2019" class="gt_row gt_right">15,030</td>
<td headers="stub_1_171 an2021" class="gt_row gt_right">16,342</td>
<td headers="stub_1_171 diff_abs2019" class="gt_row gt_right">4,900</td>
<td headers="stub_1_171 diff_abs2021" class="gt_row gt_right">6,212</td>
<td headers="stub_1_171 diff_rel2019" class="gt_row gt_right">48.37%</td>
<td headers="stub_1_171 diff_rel2021" class="gt_row gt_right">61.32%</td>
<td headers="stub_1_171 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.14' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_172" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_172 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.307</td>
<td headers="stub_1_172 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-emploi et d'assurance-parentale du Québec</td>
<td headers="stub_1_172 an2010" class="gt_row gt_right">417</td>
<td headers="stub_1_172 an2019" class="gt_row gt_right">756</td>
<td headers="stub_1_172 an2021" class="gt_row gt_right">709</td>
<td headers="stub_1_172 diff_abs2019" class="gt_row gt_right">339</td>
<td headers="stub_1_172 diff_abs2021" class="gt_row gt_right">292</td>
<td headers="stub_1_172 diff_rel2019" class="gt_row gt_right">81.29%</td>
<td headers="stub_1_172 diff_rel2021" class="gt_row gt_right">70.02%</td>
<td headers="stub_1_172 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='3.60' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_173" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_173 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.308</td>
<td headers="stub_1_173 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cotisations à des caisses de retraite ou de pension</td>
<td headers="stub_1_173 an2010" class="gt_row gt_right">2,529</td>
<td headers="stub_1_173 an2019" class="gt_row gt_right">3,775</td>
<td headers="stub_1_173 an2021" class="gt_row gt_right">4,126</td>
<td headers="stub_1_173 diff_abs2019" class="gt_row gt_right">1,246</td>
<td headers="stub_1_173 diff_abs2021" class="gt_row gt_right">1,597</td>
<td headers="stub_1_173 diff_rel2019" class="gt_row gt_right">49.27%</td>
<td headers="stub_1_173 diff_rel2021" class="gt_row gt_right">63.15%</td>
<td headers="stub_1_173 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.18' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_174" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_174 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.309</td>
<td headers="stub_1_174 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Contrats de rentes et argent transféré à des FERR</td>
<td headers="stub_1_174 an2010" class="gt_row gt_right">96</td>
<td headers="stub_1_174 an2019" class="gt_row gt_right">-</td>
<td headers="stub_1_174 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_174 diff_abs2019" class="gt_row gt_right">-</td>
<td headers="stub_1_174 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_174 diff_rel2019" class="gt_row gt_right">-</td>
<td headers="stub_1_174 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_174 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'></g></svg></td></tr>
    <tr><th id="stub_1_175" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_175 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.41.310</td>
<td headers="stub_1_175 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Primes d'assurance-vie, d'assurances temporaires et d'assurances mixtes</td>
<td headers="stub_1_175 an2010" class="gt_row gt_right">587</td>
<td headers="stub_1_175 an2019" class="gt_row gt_right">656</td>
<td headers="stub_1_175 an2021" class="gt_row gt_right">587</td>
<td headers="stub_1_175 diff_abs2019" class="gt_row gt_right">69</td>
<td headers="stub_1_175 diff_abs2021" class="gt_row gt_right">0</td>
<td headers="stub_1_175 diff_rel2019" class="gt_row gt_right">11.75%</td>
<td headers="stub_1_175 diff_rel2021" class="gt_row gt_right">0.00%</td>
<td headers="stub_1_175 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='0.52' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_176" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_176 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311.312</td>
<td headers="stub_1_176 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux en argent à des personnes habitant au Canada</td>
<td headers="stub_1_176 an2010" class="gt_row gt_right">257</td>
<td headers="stub_1_176 an2019" class="gt_row gt_right">616</td>
<td headers="stub_1_176 an2021" class="gt_row gt_right">389</td>
<td headers="stub_1_176 diff_abs2019" class="gt_row gt_right">359</td>
<td headers="stub_1_176 diff_abs2021" class="gt_row gt_right">132</td>
<td headers="stub_1_176 diff_rel2019" class="gt_row gt_right">139.69%</td>
<td headers="stub_1_176 diff_rel2021" class="gt_row gt_right">51.36%</td>
<td headers="stub_1_176 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='6.19' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_177" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_177 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311.313</td>
<td headers="stub_1_177 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Cadeaux en argent à des personnes habitant à l'extérieur du Canada</td>
<td headers="stub_1_177 an2010" class="gt_row gt_right">81</td>
<td headers="stub_1_177 an2019" class="gt_row gt_right">127</td>
<td headers="stub_1_177 an2021" class="gt_row gt_right">105</td>
<td headers="stub_1_177 diff_abs2019" class="gt_row gt_right">46</td>
<td headers="stub_1_177 diff_abs2021" class="gt_row gt_right">24</td>
<td headers="stub_1_177 diff_rel2019" class="gt_row gt_right">56.79%</td>
<td headers="stub_1_177 diff_rel2021" class="gt_row gt_right">29.63%</td>
<td headers="stub_1_177 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.51' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_178" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_178 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.311.314</td>
<td headers="stub_1_178 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Pensions alimentaires</td>
<td headers="stub_1_178 an2010" class="gt_row gt_right">152</td>
<td headers="stub_1_178 an2019" class="gt_row gt_right">229</td>
<td headers="stub_1_178 an2021" class="gt_row gt_right">84</td>
<td headers="stub_1_178 diff_abs2019" class="gt_row gt_right">77</td>
<td headers="stub_1_178 diff_abs2021" class="gt_row gt_right">−68</td>
<td headers="stub_1_178 diff_rel2019" class="gt_row gt_right">50.66%</td>
<td headers="stub_1_178 diff_rel2021" class="gt_row gt_right">−44.74%</td>
<td headers="stub_1_178 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.38' y='0.89' width='2.24' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="stub_1_179" scope="row" class="gt_row gt_left gt_stub"></th>
<td headers="stub_1_179 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right">1.42.315</td>
<td headers="stub_1_179 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center">Dons de bienfaisance</td>
<td headers="stub_1_179 an2010" class="gt_row gt_right">255</td>
<td headers="stub_1_179 an2019" class="gt_row gt_right">244</td>
<td headers="stub_1_179 an2021" class="gt_row gt_right">-</td>
<td headers="stub_1_179 diff_abs2019" class="gt_row gt_right">−11</td>
<td headers="stub_1_179 diff_abs2021" class="gt_row gt_right">-</td>
<td headers="stub_1_179 diff_rel2019" class="gt_row gt_right">−4.31%</td>
<td headers="stub_1_179 diff_rel2021" class="gt_row gt_right">-</td>
<td headers="stub_1_179 DUPE_COLUMN_PLT" class="gt_row gt_left"><?xml version='1.0' encoding='UTF-8' ?><svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' class='svglite' width='113.39pt' height='14.17pt' viewBox='0 0 113.39 14.17'><defs>  <style type='text/css'><![CDATA[    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {      fill: none;      stroke: #000000;      stroke-linecap: round;      stroke-linejoin: round;      stroke-miterlimit: 10.00;    }    .svglite text {      white-space: pre;    }  ]]></style></defs><rect width='100%' height='100%' style='stroke: none; fill: none;'/><defs>  <clipPath id='cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw=='>    <rect x='0.00' y='0.00' width='113.39' height='14.17' />  </clipPath></defs><g clip-path='url(#cpMC4wMHwxMTMuMzl8MC4wMHwxNC4xNw==)'><rect x='9.19' y='0.89' width='0.19' height='12.40' style='stroke-width: 1.07; stroke: none; stroke-linecap: butt; stroke-linejoin: miter; fill: #2FA4E7;' /><line x1='9.38' y1='14.17' x2='9.38' y2='0.0000000000000018' style='stroke-width: 1.07; stroke-linecap: butt;' /></g></svg></td></tr>
    <tr><th id="grand_summary_stub_1" scope="row" class="gt_row gt_left gt_stub gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">Total</th>
<td headers="grand_summary_stub_1 hierarchie_pour_depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 depenses_des_menages_categories_de_niveau_sommaire" class="gt_row gt_center gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 an2010" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">61,235</td>
<td headers="grand_summary_stub_1 an2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">83,822</td>
<td headers="grand_summary_stub_1 an2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">83,008</td>
<td headers="grand_summary_stub_1 diff_abs2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">16,761</td>
<td headers="grand_summary_stub_1 diff_abs2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">18,150</td>
<td headers="grand_summary_stub_1 diff_rel2019" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 diff_rel2021" class="gt_row gt_right gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td>
<td headers="grand_summary_stub_1 DUPE_COLUMN_PLT" class="gt_row gt_left gt_grand_summary_row gt_first_grand_summary_row gt_last_summary_row">—</td></tr>
  </tbody>
  
  
</table>
</div>
```


:::
:::