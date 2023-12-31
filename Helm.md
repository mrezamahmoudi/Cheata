# Chart Management

#### Creates a chart directory along with the common files and directories used in a chart.

> helm create <name>
#### Packages a chart into a versioned chart archive file.

> helm package <chart-path>
#### Run tests to examine a chart and identify possible issues:

> helm lint <chart>
#### Inspect a chart and list its contents:

> helm show all <chart>
#### Displays the contents of the values.yaml file

> helm show values <chart>
#### Download/pull chart

> helm pull <chart>
#### If set to true, will untar the chart after downloading it

> helm pull <chart> --untar=true
#### Verify the package before using it

> helm pull <chart> --verify
#### Default-latest is used, specify a version constraint for the chart version to use

> helm pull <chart> --version <number>
#### Display a list of a chart’s dependencies:

> helm dependency list <chart>