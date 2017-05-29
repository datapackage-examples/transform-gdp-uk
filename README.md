This is an example Data Package to demonstrate how data transforms work. In this example, we explain how aggregation can be done before data package gets rendered in showcase page. It assumes publisher is already familiar with Data Packages and views specifications (`views` property in Data Package specifications).

### Transforming data

Data transforms are specified in `resources` property in `views`. Each resource is an object that contains following attributes:

* `"specType": "table"` - this way we define the view as a table (other options are `"simple"` (renders a graph and accepts Plotly spec) and `"vega"` (renders a graph and accepts Vega spec)).
* `"resources"` property is an array of objects in this case, where publishers can define data transforms they want to apply.
* `"name"` - name of the resource as a reference.
* `"transform"` - array of transforms. Each transform is an object, which properties vary depending on transform type. Only common property is `"type"` that is used to specify transform type.

### Aggregating data

Under the graph on the top of this page, you can find a table that displays aggregated data. Raw data is displayed in preview section. As you can see we are aggregating "GDP" column to find its min value and "GDP_Change" column for max value. This is described in the second view object of `views` property:

* `"type": "aggregate"` - this way we define the transform to be an aggregation.
* `"fields"` - list of fields for which data aggregation will be applied.
* `"operations"` - list of operation names according to list of fields. Options are: `"sum"`, `"min"`, `"max"`, `"count"`, etc. For full reference see https://vega.github.io/vega/docs/transforms/aggregate/#ops .

### Descriptor for this data package

{{ dp.json }}
