# Smunzl Helm Charts

## Documentation

1. Increase version in `Chart.yaml`

2. Update documentation:
Edit the `README.md.gotmpl` file in the chart folder and add documentation like this:
```md
{{/* Header and Version Badge */}}
{{ template "chart.header" . }} 
{{ template "chart.versionBadge" . }}

{{ template "chart.description" . }}
{{/* Here you can add your documentation text */}}

{{/* Don't change the last lines from here on which generate a table from values.yaml */}}
## Chart Configuration Parameters
The following table lists the configurable parameters of the chart and its default values.

{{ template "chart.valuesSection" . }}
```

3. Generate Documentation:
create docs by running:
```sh
bash scripts/helm-docs.sh
```


