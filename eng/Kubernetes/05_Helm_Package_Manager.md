# Helm Package Manager

> Reference: [helm.sh](https://helm.sh/docs/topics/charts/), [Google Cloud Training - Helm Package Manager](https://google.qwiklabs.com/focuses/1044?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=11478773), [bmc blogs - Introduction to Kubernetes Helm Charts](https://www.bmc.com/blogs/kubernetes-helm-charts/)

<br>

<br>

## What is Helm?

- It is a Kubernetes package manager
  - K8s equivalent of `yum` ,  `apt`, or `npm`!
- Helm uses a **packaging format** called `charts`
  - Here, a `chart` is a collection of files that describe k8s resources
  - A `chart` is used to **deploy** something
    - ex) memcached pod, web app w/ HTTP servers, databases, etc.
  - A `chart` is created from files organized in a specific directory tree
    - These files can be packaged into versioned archives for deployment

<br>

<br>

## The Chart File Structure

- A chart is organized as a collection of files inside a directory

- The directory name == the chart name (excluding versioning information)

  - ex) A chart describing WordPress is stored in `wordpress/`

- Inside the directory, `Helm` requires the following structure

  ```sh
  wordpress/
    Chart.yaml          # A YAML file containing information about the chart
    LICENSE             # OPTIONAL: A plain text file containing the license for the chart
    README.md           # OPTIONAL: A human-readable README file
    values.yaml         # The default configuration values for this chart
    values.schema.json  # OPTIONAL: A JSON Schema for imposing a structure on the values.yaml file
    charts/             # A directory containing any charts upon which this chart depends.
    crds/               # Custom Resource Definitions
    templates/          # A directory of templates that, when combined with values,
                        # will generate valid Kubernetes manifest files.
    templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes
  ```

  - `Helm` reserves the names of the `charts/`, `crds/`, `templates/` directories and all the file names shown in the example above

<br>

### The `Chart.yaml` File

The `Chart.yaml` file is a required component of a chart and contains the following fields

```yaml
apiVersion: The chart API version (required)
name: The name of the chart (required)
version: A SemVer 2 version (required)
kubeVersion: A SemVer range of compatible Kubernetes versions (optional)
description: A single-sentence description of this project (optional)
type: The type of the chart (optional)
keywords:
  - A list of keywords about this project (optional)
home: The URL of this projects home page (optional)
sources:
  - A list of URLs to source code for this project (optional)
dependencies: # A list of the chart requirements (optional)
  - name: The name of the chart (nginx)
    version: The version of the chart ("1.2.3")
    repository: (optional) The repository URL ("https://example.com/charts") or alias ("@repo-name")
    condition: (optional) A yaml path that resolves to a boolean, used for enabling/disabling charts (e.g. subchart1.enabled )
    tags: # (optional)
      - Tags can be used to group charts for enabling/disabling together
    import-values: # (optional)
      - ImportValues holds the mapping of source values to parent key to be imported. Each item can be a string or pair of child/parent sublist items.
    alias: (optional) Alias to be used for the chart. Useful when you have to add the same chart multiple times
maintainers: # (optional)
  - name: The maintainers name (required for each maintainer)
    email: The maintainers email (optional for each maintainer)
    url: A URL for the maintainer (optional for each maintainer)
icon: A URL to an SVG or PNG image to be used as an icon (optional).
appVersion: The version of the app that this contains (optional). Needn't be SemVer. Quotes recommended.
deprecated: Whether this chart is deprecated (optional, boolean)
annotations:
  example: A list of annotations keyed by name (optional).
```

Other fields not specified above will not be applied
