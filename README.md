# Accessible-LaTeX-Thesis-Template
A LaTeX thesis template based on amsbook class aimed at assisting authors in writing documents that can be converted to to accessible epub files.   It has been tested with [LaTeXML](https://math.nist.gov/~BMiller/LaTeXML/).  October 2025.

## Read this carefully

This template comes with no offer of support or warranty.  It is merely to be used as a starting point.  In particular using it does not mean that the resulting document will be accessible, or compliant with any standards, or compliant with any university requirements for submission.

Writing documents that are accessible requires authors to know about accessibility, and write with accessibility in mind.   For an introduction to this see the article [Accessibility for the Working Mathematician](https://arxiv.org/abs/2505.22667).

This LaTeX has been written as a bare-bones example of something that can be made to work with LaTeXML to produce accessible epub files.   But it is not foolproof, and if authors do exciting and/or unexpected things with LaTeX then it is likely that the result will not be accessible and/or LaTeXML will not work.

Some tips

- Regularly run both pdflatex and latexmlc (see below) on your document as you write it, especially if you change anything in the preamble.    Do not assume that just because pdflatex is working that the latexmlc also works.

- Take care in using different style files or adding new packages to your document.  Some will work, others may not, and even if they do work they may disrupt accessibility.  The LaTeXML documentation includes a list of [implemented styles and packages](https://math.nist.gov/~BMiller/LaTeXML/manual/included.bindings/).

- Take care in just copy/pasting other people's LaTeX code.  Such code may not have been written to work with LaTeXML, or may not have been written in an accessible way.


## How to use pdflatex to produce an pdf file
This command should work as normal from the command line (or you can use your usual LaTeX editor)
```
pdflatex thesis.tex
```

## How to use latexml to produce an epub file
Here are [Instructions on installing LaTeXMml](https://math.nist.gov/~BMiller/LaTeXML/get.html).  To run it try the following from the command line 
```
latexmlc -dest=epub thesis.tex
```
This should produce the file `thesis.epub`.  

Testing has happened with TeXLive 2025 and LaTeXml 0.8.8 all on MacOS.   The epub was working well with [EPub Viewer Pro](https://apps.apple.com/us/app/epub-viewer-pro/id1572239625).  It should work on other systems.

## Overleaf
You certainly can edit this file on overleaf, but I do not know how to run LaTeXML directly on files stored on overleaf.  Instead you will need to download your project from overleaf to run LaTeXML.

## Things that work well with LaTeXML

### Title page

The title page works with both the pdf and the epub.  LaTeXml reports that "Frontmatter will not be well-structured".  With the epub viewers I have used this has not been a problem, although for one of them the formatting was a little strange (yet the document remained accessible).

### Links

The hyperref package works to give internal an external links.  For instance

```
%Accessible/WCAG compliant
\href{https://www.uic.edu}{University of Illinois Chicago}.
```

Remember that to be accessible, the link text should give a description of the text and not just the url.  So the following gives two non accessible examples:

```
%Not accessible/WCAG compliant
The link to the University of Illinois Chicago is \href{https://www.uic.edu}{here}.
%Also not accessible/WCAG compliant
\url{https://www.uic.edu}
```

### Images

You can include JPG, JPEG or PNG images.   At present, including SVG or PDF does not allow for alternative text so would not be accessible.  See below about TikZ/xypic.

```
\begin{figure}\label{fig1}
\includegraphics[alt="Description of Image that serves the same purpose",scale=0.3]{torus.jpg}
\caption{This is a torus}
\end{figure}
```

### Equations

LaTeXML will insert MathML into the epub file for the equations.  As far as I know there is nothing else that is needed to make these equations accessible.   That said, I imagine it is possible to write equations in some non-standard way that will cause LaTeXML to not work as expected.    It is recommended to use standard LaTeX/AMS macros rather than define complicated macros yourself as these can create issue with LaTeXML.

### Bibliography

The following works

```

\begin{thebibliography}{9}


\bibitem{Hartshorne}
R.~Hartshorne, \emph{Algebraic Geometry}, Springer-Verlag, New York, 1977.

\bibitem{Mumford}
D.~Mumford, \emph{Abelian Varieties}, Oxford University Press, 1970.

\bibitem{DraismaEtAl}
J.~Draisma, E.~Horobet, G.~Ottaviani, B.~Sturmfels, and R.~R.~Thomas, 
``The Euclidean distance degree of an algebraic variety,'' 
\emph{arXiv:1309.0049} (2013).  
Available at: \href{https://arxiv.org/abs/1309.0049}{Arxiv: 1309.0049}

\end{thebibliography}

```


Note that LaTeXml does support BiBTeX with some caveats, see the [LaTeXml usage webpage](https://math.nist.gov/~BMiller/LaTeXML/manual/commands/latexml.html) for details.

BibLaTeX support is being worked on [LaTeXML/issues/373](https://github.com/brucemiller/LaTeXML/issues/373)

### Code

The following package and sample work with LaTeXml.   The output looks to me to be highly accessible (but if somebody is being really fussy I am not sure it is completely WCAG compliant)

```
\usepackage{listings} 

\begin{lstlisting}[basicstyle = \ttfamily\small,resetmargins=true,tabsize=5,extendedchars=false]
def factorial(n):
    """Compute the factorial of n recursively."""
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

print(f"5! = {factorial(5)}")
\end{lstlisting}
```

## Things that do not work (or could work better) with LaTeXml

### Author field in epub

The author field is not included in the epub metadata [LaTeXML/issues/1947](https://github.com/brucemiller/LaTeXML/issues/1947).  This does not seem to matter for WCAG compliance, but I had one epub reader complain about this.

### TikZ and xypic
It is not possible to have alternative text with LaTeXml when using tikz or xypic directly [LaTeXML/issues/2165](https://github.com/brucemiller/LaTeXML/issues/2165).  Instead authors should create a standalone document.  For instance this document could be

```
\documentclass{standalone}
\usepackage[all]{xy}

\begin{document}

% Snake lemma diagram
\xymatrix{
 & 0 \ar[d] & 0 \ar[d] & 0 \ar[d] & \\
0 \ar[r] & A' \ar[r]^{f'} \ar[d]_{a} & B' \ar[r]^{g'} \ar[d]_{b} & C' \ar[r] \ar[d]_{c} & 0 \\
0 \ar[r] & A \ar[r]^f \ar[d]_{a''} & B \ar[r]^g \ar[d]_{b''} & C \ar[r] \ar[d]_{c''} & 0 \\
0 \ar[r] & A'' \ar[r]^{f''} \ar[d] & B'' \ar[r]^{g''} \ar[d] & C'' \ar[r] \ar[d] & 0 \\
 & 0 & 0 & 0 &
}

\end{document}
```

Then run the following commands
```
latex figure.tex
dvipng figure.dvi -o figure.png
```
This will create an PNG of the figure that can be included as follows

```
\begin{figure}\label{fig2}
\includegraphics[alt="Description of Figure that serves the same purpose",scale=0.3]{figure.png}
\caption{This is a figure}
\end{figure}
```



## How to use TexML
Nothing here for now!
