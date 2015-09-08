# UMD LaTeX Template

Originally from: [Thesis/Dissertation Templates from IREAP](http://www.ipr.umd.edu/resources/thesis-templates#latex)

The original LaTeX thesis template files were developed by Dorothea Brosius in 2004 as a result of several requests from graduate students writing their dissertations.   The template now in use was updated in January 2015. The software used for Windows-based PC's can be PCTEX, Miktex and WinEdt; Apple users can use Texshop.  Although the sample documents were based on parts of the thesis of Bhaskar Khubchandani, who received his Ph.D. from the University of Maryland, College Park in the Spring of 2004, the template has been updated and follows "[The University of Maryland Electronic Thesis and Dissertation (ETD) Style Guide](http://www.gradschool.umd.edu/sites/gradschool.umd.edu/files/uploads/etd_style_guide_2014.pdf)" (pdf).  In addition, the Table of Contents, the List of Figures, the List of Tables, and the Bibliography are now single-spaced; the main text is double-spaced.

The current mainthesis.tex uses the hyperref package which links items in your Table of Contents, List of Figures, and List of Tables to corresponding sections in your thesis.   The links will show in blue when you save your thesis as a pdf file.  

Please email [dbrosius@umd.edu](dbrosius@umd.edu) if you are actually using the LaTeX template (for my records) and also if you have any problems when submitting your thesis to the Graduate School (margins, indentations, etc.) so adjustments can be made to the template.

All of the files needed for your dissertation can be found in [LatexTemplateFiles-2015.zip](http://www.ipr.umd.edu/sites/default/files/documents/theses/LatexTemplateFiles-2015.zip). All of the files should be placed in the folder with your thesis files. Thesis.cls should not be changed. Mainthesis.tex should not be changed unless you include tables in your thesis, in which case you should delete the % sign on the listoftables line and the newpage line.

Insert your own text and figures in the following files: abstract.tex, titlepage.tex, copyright.tex, acknowledgements.tex, dedication.tex, foreword.tex, chapter1.tex, chapter2.tex, etc., appendix.tex, and bibliography.tex. I have included Bhaskar's .eps files from Chapter 2. If you pdf the files as they are, you can see exactly how a thesis using this template will look. The information in Chapter 2 and the Appendix is identical; I simply copied the text to show the difference between the numbering in a chapter and an appendix.

These files contain examples of several types of displayed equations (including arrays), as well as enumerated lists, theorems, axioms, references, tables, and displayed figures.

Please note that you must Latex "mainthesis.tex" twice so the references will be properly shown in the dvi file. The dvi file must be changed to a pdf file before it can be submitted to the Graduate Office.

We hope these files will be useful to you. If you need additional assistance or if this information is unclear, please contact [Dottie Brosius](dbrosius@umd.edu) at dbrosius at umd.edu or 301-405-4955.

## LaTeX "How To" Documents

Thanks to Ryan Clary, Ph.D., 2009, for finding this 13-page document on the web explaining several features of LaTex: "[LaTex--A Typesetting Program](http://www.jgsee.kmutt.ac.th/exell/General/LaTeX.html)".

Another resource, recommended by Dr. Nicholas Mecholsky, Ph.D., 2010, is "[The Not So Short Introduction to LaTex 2ε](http://mirrors.ibiblio.org/CTAN/info/lshort/english/lshort.pdf)" (pdf), by Tobias Oetiker, et al.

## Using Bibtex

Using Bibtex with LaTeX documents is not difficult. The bulk of the work is organizing your Bibtex file, which is a data base compiled by you of the articles, books, etc. which you use in the bibliographies or reference sections of your publications. The file BibtexSamples.tex contains examples of information needed for the different types of references you may wish to use (e.g., articles in refereed journals, books, uinpublished articles, conference proceedings).

Please read the file "[bibtex-instructions.pdf](http://www.ipr.umd.edu/sites/default/files/documents/theses/bibtex-instructions.pdf)". The first two pages explain how to set up and run Bibtex; the remaining pages were taken from a published article and show how the references were cited in the .tex file. The files bibtex-instructions.tex, galactic.bib, and bibtex-samples.tex are the original .tex files used with bibtex-instructions.pdf. The files diorio.bib and griem-bibtex.bib will be helpful when you are using Bibtex.
