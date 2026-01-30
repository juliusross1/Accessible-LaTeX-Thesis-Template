# Accessible-LaTeX-Thesis-Template
A LaTeX thesis template based on amsbook class aimed at assisting authors in writing documents that can be converted to to accessible epub files.  Consider this as beta.  It is designed to be used with both standard pdflatex/lualatex and [LaTeXML](https://math.nist.gov/~BMiller/LaTeXML/).

I welcome more testing and feedback, especially around conversations concerning "reasonable" things that authors are trying to do with this template.

## Read this carefully

This template comes with no offer of support or warranty.  It is merely to be used as a starting point.  In particular using it does not mean that the resulting document will be accessible, or compliant with any standards, or compliant with any university requirements for submission.

Writing documents that are accessible requires authors to know about accessibility, and write with accessibility in mind.   For an introduction to this see the article [Accessibility for the Working Mathematician](https://arxiv.org/abs/2505.22667).

This LaTeX template has been written as a bare-bones example of something that can be made to work with LaTeXML to produce accessible epub files.   But it is not foolproof, and if authors do exciting and/or unexpected things with LaTeX then it is likely that the result will not be accessible and/or LaTeXML will not work.

Some tips

- Regularly run both pdflatex and latexmlc (see below) on your document as you write it, especially if you change anything in the preamble.    Do not assume that just because pdflatex is working that the latexmlc also works as expected.

- Take care in using different style files or adding new packages to your document.  Some will work, others may not, and even if they do work they may disrupt accessibility.  The LaTeXML documentation includes a list of [implemented styles and packages](https://math.nist.gov/~BMiller/LaTeXML/manual/included.bindings/).  Note that even if a package is listed as having bindings it does not necessarily mean that every feature in that package works precisely as expected.

- Take care in just copy/pasting other people's LaTeX code.  Such code may not have been written to work with LaTeXML, or may not have been written in an accessible way.

- Just because LaTeXML works (possible without warnings) does not automatically mean that your document is accessible and/or WCAG compliant.  Author expertise is key, but see below about automatic testing tools.

## UIC Style Guide
This template was designed for those at the University of Illinois Chicago (UIC).  Others who use it may need to make changes to fit their institution's requirements (in particular to the title page).

I have run this past the UIC graduate college and they told me that they will accept this thesis even though it does not conform to every detail of the UIC Thesis Style Guide (which I understand is currently being revised)

## How to produce an pdf file

Download thesis.tex and latexml.sty and torus.jpg and figure.png into your working directory.

This command should work as normal from the command line (or you can use your usual LaTeX editor)
```
pdflatex thesis.tex
```
or
```
lualatex thesis.tex
```

As usual, you may need to run pdflatex twice to update the tableofcontents or listoffigures.

## How to use latexml to produce an epub file
  To run it try the following from the command line 
```
latexmlc -dest=thesis.epub thesis.tex
```
This should produce the file `thesis.epub`.  

Testing has happened with TeXLive 2025 and LaTeXml 0.8.8 on MacOS, Linux and Windows.    The epub was working well with [EPub Viewer Pro](https://apps.apple.com/us/app/epub-viewer-pro/id1572239625) as well as the [EpubPup Chrome Extension](https://chromewebstore.google.com/detail/epubpup-epub-reader/kjfhlbghiagglcldmlfmpkdgmehmhfjc)  It should work with other epub readers.

## GitHub and Overleaf Integration

You can certainly use Overleaf to edit your LaTeX files, but it is not possible to run LaTeXML directly within overleaf.

With a little bit of effort it is possible to run LaTeXML directly within Github so you do not have to install this software on your own machine.   Also if you have a premium Overleaf subscription you can connect Overleaf to github.  See the [Instructions on GitHub and Overleaf Integration](LaTeXMLonGitHub.md) for details.

For instance this [repository has the template in html format](https://juliusross1.github.io/Accessible-LaTeX-Thesis-Template/).  For a thesis you probably only want to use this to make sure things are working as you expect, but if you intend to distrubute this html output you might want to improve the look by creating a style.css that suits your needs.

## Installing LaTeXML

Here are [Instructions on installing LaTeXMl](https://math.nist.gov/~BMiller/LaTeXML/get.html).

The Windows instructions on the LaTeXML website do not seem to work for everyone.  I was able to install LaTeXML v0.8.8 through [anaconda](https://www.anaconda.com/download) with the following commands

```
conda create -n latexml
conda activate latexml
conda install perl-latexml --channel conda-forge --channel feng1m8
```

See https://github.com/feng1m8/latexml-conda

## LaTeXML Warnings
LaTeXML can produce a lot of warnings.  The ones that say "MathParser failed" will not affect the rendering of the mathematics equations, so that error will not prevent the document produced from being accessible/compliant (see (https://github.com/brucemiller/LaTeXML/issues/2742#issuecomment-3755332817))

## Testing Epub files for accessibility

No tool will be perfect it telling you if your document is fully accessible, but there are good tools that will indicate problems.  For instance you can try [Ace by Daisy](https://daisy.org/activities/software/ace/) which will check various standards.  If you are in the US note that new regulations for state institutions require WCAG compliance.

When I ran this on thesis.epub it reported only one WCAG non-compliance issue [LaTeXML/issues/2661](https://github.com/brucemiller/LaTeXML/issues/2661)

## Things that work well with LaTeXML

### Title page

The title page works with both the pdf and the epub.  LaTeXml reports that "Frontmatter will not be well-structured".  With the epub viewers I have used this has not been a problem, although for one of them the formatting was a little strange (yet the document remained accessible).

### Links

The hyperref package works to give internal and external links.  For instance

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

### Commutative diagrams

The amscd package is supported, and I am not aware of any issues with it when you use the amsbook class as in this template.   I note that amscd does not allow for diagonal arrows 

I am not aware of a way to make complicated commutative diagrams truely accessible; making them in tikz-cd and using alt-text as described below will be compliant, but likely not very accessible unless the diagram is simple.   Consider if you can use amscd instead.

### Images

You can include JPG, JPEG or PNG images.   At present, including SVG or PDF does not allow for alternative text so would not be accessible.  See below about TikZ/xypic.

```
\begin{figure}\label{fig1}
\includegraphics[alt="Description of Image that serves the same purpose",scale=0.3]{torus.jpg}
\caption{This is a torus}
\end{figure}
```

### Comments on Accessible Images

AI tools can be good at helping you write alt-text (you can even paste in the entire tikz code and ask it to give you an alt text or paste in the picture)  but do read the output since AI can sometimes generate nonsense.  The alt-text is meant to be short, so see the article above for what is expected when long alt texts are needed for complicated images.

I add that even though alt-text for mathematical figures may satisfy compliance, it is likely not very accessible.   I put in here a [plug for PreFigure](https://prefigure.org/) even though I do not see a practical way to use that software with this template.

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


Note that LaTeXml does support BiBTeX but there are caveats and my recommendation is you do not try this;  see the [LaTeXml usage webpage](https://math.nist.gov/~BMiller/LaTeXML/manual/commands/latexml.html) for details.

BibLaTeX support is being worked on [LaTeXML/issues/373](https://github.com/brucemiller/LaTeXML/issues/373)

### Code

The following package and sample work with LaTeXML.   The output looks to me to be highly accessible (but if somebody is being really fussy I am not sure it is completely WCAG compliant)

```
\usepackage{listings} 

\begin{lstlisting}[basicstyle = \singlespacing\ttfamily\small,resetmargins=true,tabsize=5,extendedchars=false]
def factorial(n):
    """Compute the factorial of n recursively."""
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

print(f"5! = {factorial(5)}")
\end{lstlisting}
```

## Things that do not work (or could work better) with LaTeXML

### Footnotes

I understand that footnotes do not work at all in epub (but do work in html).  It is recommended to avoid them completely.

### \mathcal vs \mathscr

There is not support to differentiate between \mathscr and \mathcal. This is being worked on [https://github.com/brucemiller/LaTeXML/pull/2244](https://github.com/brucemiller/LaTeXML/pull/2244).   I recommend that you only use one of these throughout.  

In more detail: \mathcal{A} is considered a variant of \mathscr{A} with a different visual appearance but the same *meaning*.  I particular you should avoid using these in a way that the difference changes the meaning.  So, for example, you end up writing something like \mathcal{A} = \mathscr{A} + 1 then you have done something wrong and should pick different notation!

### Author field in epub

The author field is not included in the epub metadata [LaTeXML/issues/1947](https://github.com/brucemiller/LaTeXML/issues/1947).  This does not seem to matter for WCAG compliance, but I had one epub reader complain about this.

### TikZ and xypic
It is not possible to have alternative text with LaTeXML when using tikz or xypic directly [LaTeXML/issues/2165](https://github.com/brucemiller/LaTeXML/issues/2165).  Instead authors should create a standalone document.  For instance this document could be

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
latex diagram.tex
dvipng diagram.dvi -o diagram.png
```

If that does not work well for you then you can try this
```
lualatex diagram.tex
pdftoppm -png diagram.pdf diagram
```

This will create an PNG of the figure that can be included in the following way.

```
\includegraphics[alt="Description of image that serves the same purpose",scale=0.3]{diagram.png}

```

It might be that you want this as a "figure" at which point the software will place the figure in an appropriate place.   I am not sure if placement might be different between the pdf and epub files.

```
\begin{figure}\label{fig2}
\includegraphics[alt="Description of image that serves the same purpose",scale=0.3]{diagram.png}
\caption{This is a figure}
\end{figure}
```

### TikZ and xypic mathematical formulae

It is most accessible if you write your equations using usual LaTeX commands.  If you have a complicated or non-standard equation for which you need to use tikz (this is likely not to happen often) you might prefer to include it as follows so that equation numbering works (but this seems pretty non-standard so I recommend doing this are infrequently as possible and expect things to break)

```
\begin{equation}
\Delta = 2 + \includegraphics[alt="Description of image that serves the same purpose",scale=0.3]{mathematicaltikz.png}
\end{equation}
```
or you do this inline

```
$ X = \includegraphics[alt="Description of image that serves the same purpose",scale=0.3]{mathematicaltikz.png}$
```

### Internal References (for instance to Theorems)
When using an internal reference such as

```
\begin{theorem}\label{besttheoremever}
...
\end{theorem}
...
This is due to Theorem \ref{besttheoremever}
```

the link that appears only has the number of the theorem and not the entire "Theorem 1" link.  As such it fails [WCAG 2.4.4](https://www.wcag.com/designers/2-4-4-link-purpose-in-context/) which requires that purpose of each link can be determined from the link text alone.  For internal links I think it is reasonable to say that this has minimal impact on accessibility but others may disagree.    I do not know a good way around it  - the [zref-clever](zref-clever) package would be ideal but at this time this package does not work with LaTeXML[issue #2444](https://github.com/brucemiller/LaTeXML/issues/2444).  The [clever-ref](https://ctan.org/pkg/cleveref?lang=en) package is outdated, so is not recommended at all.

### Acknowledgements
Thanks to the LaTeXML team for creating their software without which I am not sure how our students would be able to graduate in 2026.  I thank all others I have spoken to about accessibility, including Michael Gintz who has made many positive contributions to this template.  I also thank Dan MacKinnon from the Overleaf team for creating the GitHub action.
