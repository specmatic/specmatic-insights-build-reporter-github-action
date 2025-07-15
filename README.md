# Specmatic Insights Github Action
This Github Action is used to publish the build stats to the Specmatic Insights server.

While invoking this Github Action, the following arguments must be passes:

- `specmatic-insights-host`(Optional) URL of the Specmatic Insights server. By default, this will point to https://insights.specmatic.io However if you've an on-prem Specmatic Insights server, then you can set the host accordingly.
- `specmatic-reports-dir`(Optional) Path to the Specmatic reports directory. If not specified, will default to ./build/reports/specmatic
- `org-id`(Required) Specmatic Organization ID
- `branch-name`(Required) The short branch name that triggered the build. In Github this maps to github.ref_name environment variable.
- `repo-name`(Required) Name of the GIT repository. The repo should not include the repo owner name. In Github this maps to github.event.repository.name environment variable.
- `repo-id`(Required) Unique ID of the GIT repository. In Github this maps to github.repository_id environment variable.
- `repo-url`(Required) Fully qualified HTTP GIT repository URL. In Github this maps to github.event.repository.html_url environment variable.

In your Github workflow file, please add the following step after running specmatic command:

```yaml
- name: Run Specmatic Insights Github Build Reporter
  uses: specmatic/specmatic-insights-build-reporter-github-action@v2.2.0
  with:
    org-id: ${{ secrets.SPECMATIC_ORG_ID }}
    branch-name: ${{ github.ref_name }}
    repo-name: ${{ github.event.repository.name }}
    repo-id: ${{ github.repository_id }}
    repo-url: ${{ github.event.repository.html_url }}
```

If you need to specify the addition arguments, then this is a sample:

```yaml
- name: Run Specmatic Insights Github Build Reporter
  uses: specmatic/specmatic-insights-build-reporter-github-action@v2.2.0
  with:
    org-id: ${{ secrets.SPECMATIC_ORG_ID }}
    specmatic-insights-host: https://custom-insights-service.com
    specmatic-reports-dir: ./custom/reports/dir/path
    branch-name: ${{ github.ref_name }}
    repo-name: ${{ github.event.repository.name }}
    repo-id: ${{ github.repository_id }}
    repo-url: ${{ github.event.repository.html_url }}
```
After substitution this is what it would look like:

```yaml
- name: Run Specmatic Insights Github Build Reporter
  uses: specmatic/specmatic-insights-build-reporter-github-action@v2.2.0
  with:
    org-id: '*****'
    specmatic-insights-host: https://custom-insights-service.com
    specmatic-reports-dir: ./custom/reports/dir/path
    branch-name: main
    repo-name: specmatic-order-bff-java
    repo-id: 636154288
    repo-url: https://github.com/specmatic/specmatic-order-bff-java
```
