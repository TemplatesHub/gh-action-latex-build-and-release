# LaTeX build and release
![LaTeX](https://img.shields.io/badge/latex-%23008080.svg?style=for-the-badge&logo=latex&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)   
This actions compiles a PDF document starting from LaTeX source code and attaches the PDF document as asset in a release.

## Table of contents
- [Usage example](#usage-example)
- [Optional inputs](#optional-inputs)
- [Final PDF result](#final-pdf-result)

## Usage example
This example is executed every time a new release is created, resulting in the compilation of PDF document, starting from the repository's LaTeX source code, which is then uploaded as asset in said release.
```yaml
name: LaTeX document CD
on:
  release:
    types: [created]
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
          pdf-name: 'My_pdf_document'
```

## Optional inputs
All the inputs in this action are optional.

| Input           | Type   | Default                           | Description                                                                      |
|-----------------|--------|-----------------------------------|----------------------------------------------------------------------------------|
| tex-entry-point | string | main                              | Entry point .tex file used to create the PDF (do not include the file extension) |
| pdf-name        | string | ${{github.event.repository.name}} | Final PDF file name (do not include the file extension)                          |
| gh-token        | string | ${{github.token}}                 | Token used to upload the PDF to the release                                      |

## Final PDF result
After the action has completed its execution successfully, you will find the PDF as asset in your latest release. The file name will be:  
```console
<pdf-name>-<latest tag>.pdf
```
Example (using tag v1.0.0 in the release): __"My_pdf_document-v1.0.0.pdf"__  

Please note that, unfortunately, __the white spaces in the PDF file name will be replaced with dots automatically by GitHub__.
