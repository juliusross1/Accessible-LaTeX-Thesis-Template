# Accessible-LaTeX-Thesis-Template
A LaTeX thesis template based on amsbook class aimed at assisting authors in creating documents that can create accessible epub files.

## Read This carefully

Writing documents that are accessible requires authors to know about accessibility, and write with accessibility in mind.   For an introduction to this see [Accessibility for the Working Mathematician](https://arxiv.org/abs/2505.22667)

This LaTeX has been written as a bare-bones example of something that can be made to work with LaTeXml to produce accessible epub files.   But it is not foolproof, and if authors do unexpected things with LaTeX then it is likely that the result will not be accessible and/or LaTeXml will fail.

Some tips

- It is recommended that you run both pdflatex and latexmlc (see below) on this document as you write it.  Do not assume that just because pdflatex is working that the latexmlc also works.

- Take care in adding new packages to your document.  Some will work, others may not, and even if they do work they may disrupt accessibility.

- Take care in just copy/pasting other people's LaTeX code.  Such code may not have been written to work with LaTeXml, or may not have been written in an accessible way.