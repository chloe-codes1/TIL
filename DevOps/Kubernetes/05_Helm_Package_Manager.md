# Helm Package Manager

> Reference: [helm.sh](https://helm.sh/docs/topics/charts/), [Google Cloud Training - Helm Package Manager](https://google.qwiklabs.com/focuses/1044?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=11478773), [bmc blogs - Introduction to Kubernetes Helm Charts](https://www.bmc.com/blogs/kubernetes-helm-charts/)

<br>

<br>

## What is Helm?

- Kubernetes package manager이다
  - K8s equivalent of `yum` ,  `apt`, or `npm`!
- Helm은 `charts`라는 **packaging format**을 사용한다
  - 여기서 `chart`는 k8s resources를 describe하는 file들의 집합이다
  - `chart`는 무언가를 **배포**하기 위해 사용된다
    - ex) memcached pod, web app w/ HTTP servers, databases, etc.
  - `chart`는 특정 directory tree로 구성된 file들로 생성되어 있다
    - 이 file들은 배포될 version의 archive로 packaging 될 수 있다

<br>

<br>

## The Chart File Structure

- Chart는 directory 내부에 일련의 파일들로 구성되어 있다

- Directory의 이름 == chart 이름 (versioning 정보를 제외한)이다

  - ex) WordPress를 describe 하는 chart는 `wordpress/`에 저장된다

- Directory 내부에, `Helm`은 아래의 구조를 필요로 한다

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

  - `Helm`은  `charts/`, `crds/`, `templates/` directory와 위의 예시에 나와있는 모든 파일들의 이름을 예약하여 사용한다 

<br>

### The `Chart.yaml` File

`Chart.yaml` file은 chart의 필수 구성 요소이며, 아래의 fields를 포함하고 있다

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

위에 명시되어 있지 않은 다른 fields는 적용되지 않는다

