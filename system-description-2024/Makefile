# the name of the output
CO=main
# names of files other than sources the change of which should recompile the
# source
#CHANGED_FILES_OTHER =literature.bib
CHANGED_FILES_OTHER+=$(wildcard *.tex) $(wildcard *.bib) $(wildcard sections/*.tex)
CHANGED_FILES_OTHER+=$(wildcard figs/*)

# List of TeX files
#TEX_FILES=$(wildcard *.tex)

###############################################################################
#                                 Rules                                       #
###############################################################################

.PHONY: all clean zip

all: $(CO).pdf

$(CO).pdf: $(CO).tex $(CHANGED_FILES_OTHER)
#	pdflatex $(CO)
#	bibtex $(CO)
#	pdflatex $(CO)
#	pdflatex $(CO)
	rubber --unsafe --synctex --pdf $<
#	rubber-info --errors $<
#	rubber-info --check $<

zip:
	zip -r buchi-sky-is-not.zip figs/ literature.bib llncs.cls macros.tex *.tex Makefile splncs.bst main.bbl

clean:
	rm -f *.dvi *.log $(CO).blg $(CO).bbl $(CO).toc *.aux $(CO).out $(CO).lof
	rm -f $(CO).pdf
	rm -f $(CO).rubbercache
	rm -f *~
