TARGET=prelim

BIBTEX=bibtex
LATEX=latexmk
SPELLCHECK=aspell
VIEWER=open -a Preview

main: $(TARGET).pdf

spell:
	$(SPELLCHECK) -c $(TARGET).tex

view: $(TARGET).pdf
	$(VIEWER) $(TARGET).pdf

$(TARGET).pdf: $(TARGET).tex $(TARGET).bbl
	$(LATEX) -pdf $(TARGET).tex

$(TARGET).bbl: $(TARGET).bib $(TARGET).aux
	$(BIBTEX) $(TARGET)
	$(LATEX) -pdf $(TARGET).tex

$(TARGET).aux: $(TARGET).tex
	$(LATEX) -pdf $(TARGET).tex

clean:
	latexmk -C

.PHONY: all view spell clean
