# Accessible-LaTeX-Thesis-Template
A LaTeX thesis template based on amsbook class aimed at assisting authors in creating documents that can create accessible epub files.

## Read this carefully

Writing documents that are accessible requires authors to know about accessibility, and write with accessibility in mind.   For an introduction to this see the article [Accessibility for the Working Mathematician](https://arxiv.org/abs/2505.22667).

This LaTeX has been written as a bare-bones example of something that can be made to work with LaTeXml to produce accessible epub files.   But it is not foolproof, and if authors do unexpected things with LaTeX then it is likely that the result will not be accessible and/or LaTeXml will fail.

Some tips

- It is recommended that you run both pdflatex and latexmlc (see below) on this document as you write it.  Do not assume that just because pdflatex is working that the latexmlc also works.

- Take care in adding new packages to your document.  Some will work, others may not, and even if they do work they may disrupt accessibility.

- Take care in just copy/pasting other people's LaTeX code.  Such code may not have been written to work with LaTeXml, or may not have been written in an accessible way.


## How to use latexml
Here are [Instructions on installing LaTeXMml](https://math.nist.gov/~BMiller/LaTeXML/get.html).  To run it on this document try
```
latexmlc -dest=epub thesis.tex
```
This should produce the file `thesis.epub`.  

Testing has happened with TeXLive 2025 and LaTeXml 0.8.8 all on MacOS.   The epub was working well with [EPub Viewer Pro](https://apps.apple.com/us/app/epub-viewer-pro/id1572239625).  It should work on other systems.


## How to use TexML
Nothing here for now

## Things that work

### Title page
### Links
### Images
### Equations

## Things that do not work or could work better

### Author field in epub
### Including pdf images
### \usepackage{babel}
### TikZ and xypic