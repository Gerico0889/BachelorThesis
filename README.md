Written entirely in org-mode using
[Mimosis](https://github.com/Submanifold/latex-mimosis) class.

## General info
The (PPLite)[http://www.cs.unipr.it/~zaffanella/PPLite/] is an open-source C++ library implementing the abstract domain of convex polyhedra, to be used in tools for static analysis and verification.

My work was to implement cartesian factory in order to improve performances.

## Compiling

To compile add this to your emacs init file:

``` emacs-lisp
;; Custom LaTeX classes
(add-to-list 'org-latex-classes
                 '("mimosis"
                   "\\documentclass{mimosis}
 [NO-DEFAULT-PACKAGES]
 [PACKAGES]
 [EXTRA]
\\newcommand{\\mboxparagraph}[1]{\\paragraph{#1}\\mbox{}\\\\}
\\newcommand{\\mboxsubparagraph}[1]{\\subparagraph{#1}\\mbox{}\\\\}"
                   ("\\chapter{%s}" . "\\chapter*{%s}")
                   ("\\section{%s}" . "\\section*{%s}")
                   ("\\subsection{%s}" . "\\subsection*{%s}")
                   ("\\subsubsection{%s}" . "\\subsubsection*{%s}")
                   ("\\mboxparagraph{%s}" . "\\mboxparagraph*{%s}")
                   ("\\mboxsubparagraph{%s}" . "\\mboxsubparagraph*{%s}")))

;; Enabling listings for LaTeX
(require 'org)
(require 'ox-latex)
(add-to-list 'org-latex-packages-alist '("" "listings"))
(setq org-latex-listings 'listings)
(setq org-latex-listings-options
        '(("style" "mystyle")))
(setq org-src-fontify-natively t)

(org-babel-do-load-languages
 'org-babel-load-languages
 '((R . t)
   (latex . t)))

;; Using latexmk with bibtex to compile latex and export to pdf
(setq org-latex-pdf-process (list "latexmk -shell-escape -bibtex -f -pdf %f"))

;; RefTeX default bibliography
(setq reftex-default-bibliography '("ABSOLUTE PATH TO YOUR BIB FILE"))
```
