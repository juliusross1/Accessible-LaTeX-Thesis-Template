# Accessible-LaTeX-Thesis-Template
A LaTeX thesis template based on amsbook class aimed at assisting authors in creating documents that can create accessible epub files.

## Read this carefully

This template comes with no offer of support or warranty.  It is merely to be used as a starting point.  In particular using it does not mean that the resulting document will be accessible, or compliant with any standards, or compliant with any university requirements for submission.

Writing documents that are accessible requires authors to know about accessibility, and write with accessibility in mind.   For an introduction to this see the article [Accessibility for the Working Mathematician](https://arxiv.org/abs/2505.22667).

This LaTeX has been written as a bare-bones example of something that can be made to work with LaTeXml to produce accessible epub files.   But it is not foolproof, and if authors do exciting and/or unexpected things with LaTeX then it is likely that the result will not be accessible and/or LaTeXml will not work.

Some tips

- Regularly run both pdflatex and latexmlc (see below) on your document as you write it, especially if you change anything in the preamble.    Do not assume that just because pdflatex is working that the latexmlc also works.

- Take care in using different style files or adding new packages to your document.  Some will work, others may not, and even if they do work they may disrupt accessibility.

- Take care in just copy/pasting other people's LaTeX code.  Such code may not have been written to work with LaTeXml, or may not have been written in an accessible way.


## How to use pdflatex to produce an pdf file
This should work as normal
```
pdflatex thesis.tex
```

## How to use latexml to produce an epub file
Here are [Instructions on installing LaTeXMml](https://math.nist.gov/~BMiller/LaTeXML/get.html).  To run it on this document from the command line run
```
latexmlc -dest=epub thesis.tex
```
This should produce the file `thesis.epub`.  

Testing has happened with TeXLive 2025 and LaTeXml 0.8.8 all on MacOS.   The epub was working well with [EPub Viewer Pro](https://apps.apple.com/us/app/epub-viewer-pro/id1572239625).  It should work on other systems.



## Things that work well with LaTeXml

### Title page

The title page works with both the pdf and the epub.  LaTeXml reports that "Frontmatter will not be well-structured".  With the epub viewers I have used this has not been a problem, although for one of them the formatting was a little strange (yet the document remained accessible).

### Links

### Images

### Equations

## Bibliography

## Code

## Things that do not work (or could work better) with LaTeXml

### Author field in epub
### Including pdf images
### \usepackage{babel}
### TikZ and xypic
It is not possible at the moment to have alternative text when using tikz or xypic directly.  Instead authors should create a standalone document with that figure and run the following commands
```
latex figure.tex
dvisvgm figure.dvi
```
This will create an SVG of the figure that can be included as described above.



## How to use TexML
Nothing here for now!