---
title: "observable js test"
description: |
  description
author: Simon Coulombe
date: 2024-04-28
categories: []
lang: fr
---









# observable js   


https://quarto.org/docs/interactive/ojs/







:::::{.cell}

```{.js .cell-code .hidden code-fold="undefined" startFrom="19" source-offset="0"}
penguins = FileAttachment("palmer-penguins.csv").csv({ typed: true })
```

::::{.cell-output .cell-output-display}

:::{#ojs-cell-1 nodetype="declaration"}
:::
::::
:::::

::::::{.cell}

```{.js .cell-code .hidden code-fold="undefined" startFrom="24" source-offset="-0"}
viewof bill_length_min = Inputs.range(
  [32, 50], 
  {value: 35, step: 1, label: "Bill length (min):"}
)
viewof islands = Inputs.checkbox(
  ["Torgersen", "Biscoe", "Dream"], 
  { value: ["Torgersen", "Biscoe"], 
    label: "Islands:"
  }
)
```

:::::{.cell-output .cell-output-display}

::::{}

:::{#ojs-cell-2-1 nodetype="declaration"}
:::
::::
:::::

:::::{.cell-output .cell-output-display}

::::{}

:::{#ojs-cell-2-2 nodetype="declaration"}
:::
::::
:::::
::::::

:::::{.cell}

```{.js .cell-code .hidden code-fold="undefined" startFrom="36" source-offset="0"}
filtered = penguins.filter(function(penguin) {
  return bill_length_min < penguin.bill_length_mm &&
         islands.includes(penguin.island);
})
```

::::{.cell-output .cell-output-display}

:::{#ojs-cell-3 nodetype="declaration"}
:::
::::
:::::

:::::{.cell}

```{.js .cell-code .hidden code-fold="undefined" startFrom="43" source-offset="0"}
Plot.rectY(filtered, 
  Plot.binX(
    {y: "count"}, 
    {x: "body_mass_g", fill: "species", thresholds: 20}
  ))
  .plot({
    facet: {
      data: filtered,
      x: "sex",
      y: "species",
      marginRight: 80
    },
    marks: [
      Plot.frame(),
    ]
  }
)
```

::::{.cell-output .cell-output-display}

:::{#ojs-cell-4 nodetype="expression"}
:::
::::
:::::

:::::{.cell}

```{.js .cell-code .hidden code-fold="undefined" startFrom="63" source-offset="0"}
<!-- d3 = require("d3@7") -->
topojson = require("topojson")
```

::::{.cell-output .cell-output-display}

:::{#ojs-cell-5 nodetype="declaration"}
:::
::::
:::::

:::::{.cell}

```{.js .cell-code .hidden code-fold="undefined" startFrom="69" source-offset="0"}
vegalite({
  data: {values: transformedData},
  vconcat:[{
    width: 600,
    height: 200,
    title: "Year over year change in CPI",
    config: {
      axis: {shortTimeLabels: true}
    },
    layer: [{
    mark: {type: 'line'},
    encoding: {
      x: {field: 'refPer', type: 'temporal', timeUnit: 'yearmonthdate',title:"",
         scale: {domain: {selection: "brush"}}},
      dx: {  
        field: "Series", "type": "nominal",
        scale: {"rangeStep": 6} 
      },
      color: {field: "Series", type: 'nominal',"scale": {"scheme": "Dark2"}}, 
      y: {type: 'quantitative', field: 'pct_change',axis: {format: ".1%"},title:"", "grid": false}
    }
  },
    {
      "data": {"values": [{"guide": 0}]},
      "mark": "rule",
      "encoding": {
        "y": {"field": "guide","type": "quantitative"},
        "color": {"value": "black"}
      }
    }
  ]}, {
    width: 600,
    mark: {type: 'line'},
    title: "",
    height: 60,
    encoding: {
      x: {field: 'refPer', type: 'temporal', timeUnit: 'yearmonthdate',title:""},
      color: {field: "Series", type: 'nominal',"scale": {"scheme": "Dark2"}}, 
      y: {type: 'quantitative', field: 'pct_change',axis: {format: ".1%"},title:""}
    },
    config: {
      background: "#808080",
      axis: {shortTimeLabels: true}
    },
    selection: {
      brush: {type: "interval", encodings: ["x"]}
    }
  }]})
```

::::{.cell-output .cell-output-display}

:::{#ojs-cell-6 nodetype="expression"}
:::
::::
:::::

::::::{.cell}

```{.js .cell-code .hidden code-fold="undefined" startFrom="122" source-offset="-0"}
vectors = {return {
  1159447162: "cantaloups",
  1159447163: "avocat",
}}

data = d3.json("https://www150.statcan.gc.ca/t1/wds/rest/getDataFromVectorsAndLatestNPeriods",{
        method:"POST",
      body: JSON.stringify(Object.keys(vectors).map(function(v){return {"vectorId":v, "latestN":2000}})),
  headers: {"Content-type": "application/json; charset=UTF-8"}
})
```

:::::{.cell-output .cell-output-display}

::::{}

:::{#ojs-cell-7-1 nodetype="declaration"}
:::
::::
:::::

:::::{.cell-output .cell-output-display}

::::{}

:::{#ojs-cell-7-2 nodetype="declaration"}
:::
::::
:::::
::::::

::::::{.cell}

```{.js .cell-code .hidden code-fold="undefined" startFrom="135" source-offset="-0"}
vegalite = require("@observablehq/vega-lite@0.1")
d3 = require("https://d3js.org/d3.v5.min.js")

transformedData = [].concat.apply([], data.map(function(d){
  var rows = d.object.vectorDataPoint.map(function(row){
    row.Series=vectors[d.object.vectorId];

    var year=parseInt(row.refPer.slice(0,4));
    var month=parseInt(row.refPer.slice(5,7));
    //if (month==1) {
    //  year-=1;
    //  month=12;
    //} else month-=1;
    year-=1;
    row.oldPer=''+year+'-'+(month+'').padStart(2, '0')+row.refPer.slice(7,10);
    //debugger
    row.Value=row.value*Math.pow(10,row.scalarFactorCode);
    var result = d.object.vectorDataPoint.filter(function(r) {
      return r.refPer === row.oldPer;
    });
    row.oldVal = (result[0] !== undefined) ? result[0].Value : null;
    row.change=row.Value-row.oldVal;
    row.pct_change=row.change/row.oldVal;
    row.year=year;
    return row;
  });
  return rows;
})).filter(function(row){
  return(row.oldVal!=null & row.year>=1989)
})
```

:::::{.cell-output .cell-output-display}

::::{}

:::{#ojs-cell-8-1 nodetype="declaration"}
:::
::::
:::::

:::::{.cell-output .cell-output-display}

::::{}

:::{#ojs-cell-8-2 nodetype="declaration"}
:::
::::
:::::

:::::{.cell-output .cell-output-display}

::::{}

:::{#ojs-cell-8-3 nodetype="declaration"}
:::
::::
:::::
::::::
