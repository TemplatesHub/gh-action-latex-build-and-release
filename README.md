# LaTeX build and release
![LaTeX](https://img.shields.io/badge/latex-%23008080.svg?style=for-the-badge&logo=latex&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)   
This actions compiles a PDF document starting from LaTeX source code and creates a release (using the latest tag of the repository), attaching the PDF document as asset.

## Table of contents
- [Usage example](#usage-example)
- [Optional inputs](#optional-inputs)
- [Final PDF result](#final-pdf-result)

## Usage example
This example is executed every time a new tag is pushed, resulting the creation of a new release (with said tag) containing the compiled PDF document as asset.
```yaml
name: LaTeX document CD
on:
  push:
    tags:
      - "v*.*.*"
jobs:
  build-and-release:
    runs-on: ubuntu-latest
    steps:
      - name: Set up Git repository
        uses: actions/checkout@v2
      - name: Build and release LaTeX document
        uses: TemplatesHub/gh-action-latex-build-and-release@v1
        with:
          tex-entry-point: 'main'
          pdf-name: 'My pdf document'
```
To trigger the execution, you will need to run, in order, the following commands:
```console
git tag -a v<VERSION> -m "<RELEASE NOTES>"
```
```console
git push origin --tags
```
Despite this example uses the "tag push" trigger, <ins>you can use this action in other ways, just keep in mind that the latest tag available will be used to trigger a release</ins>.

## Optional inputs
All the inputs in this action are optional.

| Input           | Type   | Default                             | Description                                               |
|-----------------|--------|-------------------------------------|-----------------------------------------------------------|
| tex-entry-point | string | main                                | Entry point .tex file for compilation (without extension) |
| pdf-name        | string | ${{ github.event.repository.name }} | PDF file name (without extension)                         |

## Final PDF result
After the action has completed its execution successfully, you will find the PDF as asset in your latest release. The file name will be:  
```console
<pdf-name><white space><latest tag>.pdf
```
Example: __"My pdf document v1.0.0.pdf"__
