This is an example dataset to demonstrate how data transforms work. In this example, we explain how to aggregate a resource. We assume a publisher is already familiar with Data Packages and views specifications (`views` property in Data Package specifications).

### Transforming data

Data transforms are specified in `resources` attribute of `views` property. Each `resource` is an object that contains following attributes:

* `"name"` - name of the resource as a reference.
* `"transform"` - array of transforms. Each transform is an object, which properties vary depending on transform type.

### Aggregating data

Under the graph on the top of this page, you can find a table that displays aggregated data. Raw data is displayed in preview section. As you can see we are aggregating "GDP" column to find its min value and "GDP_Change" column for max value. This is described in the second view object of `views` property:

```
{
  "name": "table-view-aggregation",
  "specType": "table",
  "resources": [
    {
      "name": "annual",
      "transform": [
        {
          "type": "aggregate",
          "fields": ["GDP", "GDP_Change"],
          "operations": ["min", "max"]
        }
      ]
    }
  ]
}
```

where in `transform` property:

* `"type": "aggregate"` - this way we define the transform to be an aggregation.
* `"fields"` - list of fields for which data aggregation will be applied.
* `"operations"` - list of operation names according to list of fields. Options are: `"sum"`, `"min"`, `"max"`, `"count"`, etc. For full reference see https://vega.github.io/vega/docs/transforms/aggregate/#ops .

### Descriptor for this data package

This is the full `datapackage.json` of this dataset:

```
{
  "licenses": [
    {
      "id": "odc-pddl",
      "url": "http://opendatacommons.org/licenses/pddl/"
    }
  ],
  "name": "transform-example-gdp-uk",
  "resources": [
    {
      "name": "annual",
      "path": "annual.csv",
      "schema": {
        "fields": [
          {
            "format": "any",
            "name": "Year",
            "type": "date"
          },
          {
            "description": "Gross Value Added at basic prices: chained volume measures: Seasonally adjusted. Millions of GBP in base period money. Base period=2009. ABMI variable in ONS source.",
            "name": "GDP",
            "type": "number"
          },
          {
            "description": "Gross Domestic Product: Year on Year growth: CVM SA. IHYP variable in ONS source.",
            "format": "percentage",
            "name": "GDP_Change",
            "type": "number"
          },
          {
            "description": "Gross domestic product index. Base period=2009. YBEZ variable in ONS source.",
            "name": "GDP_Index",
            "type": "number"
          }
        ]
      },
      "sources": [
        {
          "web": "http://www.ons.gov.uk/ons/datasets-and-tables/data-selector.html?cdid=ABMI&dataset=qna&table-id=C2"
        }
      ]
    }
  ],
  "sources": [
    {
      "homepage": "http://www.ons.gov.uk/ons/rel/gva/gross-domestic-product--preliminary-estimate/q4-2012/tsd---preliminary-estimate-of-gdp-q4-2012.html",
      "name": "Office for National Statistics - GDP Time Series",
      "web": "http://www.ons.gov.uk/ons/datasets-and-tables/downloads/csv.csv?dataset=pgdp"
    }
  ],
  "title": "Example Aggregation on UK Gross Domestic Product (GDP)",
  "views": [
    {
      "id": "Graph",
      "state": {
        "graphType": "columns",
        "group": "Year",
        "series": [
          "GDP_Change"
        ]
      },
      "type": "Graph"
    },
    {
      "name": "table-view-aggregation",
      "specType": "table",
      "resources": [
        {
          "name": "annual",
          "transform": [
            {
              "type": "aggregate",
              "fields": ["GDP", "GDP_Change"],
              "operations": ["min", "max"]
            }
          ]
        }
      ]
    }
  ]
}
```
