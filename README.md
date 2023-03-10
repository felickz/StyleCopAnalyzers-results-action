# StyleCop.Analyzers Results Action

This action is designed to run as part of a workflow that builds projects referencing NuGet [StyleCop.Analyzers](https://www.nuget.org/packages/StyleCop.Analyzers/)

It produces a GitHub compatible SARIF file for uploading to the repository 'Code scanning alerts'.

# Usage

See [action.yml](action.yml)

### Input Parameters

**sarif_directory**: _(optional)_ The output directory where SARIF files should be collected.

### Workflow Examples

```yaml
on:
  push:

jobs:
  SCS:
    runs-on: ubuntu-latest
    steps:     
      - uses: actions/checkout@v2
      
      - name: Set up projects
        uses: felickz/StyleCopAnalyzers-add-action@main

      - name: Build
        run: |
          dotnet restore
          dotnet build
        
      - name: Convert sarif for uploading to GitHub
        uses: felickz/StyleCopAnalyzers-results-action@v1.3
        
      - name: Upload sarif	
        uses: github/codeql-action/upload-sarif@v2
```


