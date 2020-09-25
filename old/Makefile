PAPER 		= proposal-v2
SUMMARY		= Summary
DESCRIPTION	= Description
REFERENCES	= References
PERSONNEL	= Personnel
BUDGET		= Budget
DATA		= Data
FACILITIES  = Facilities

LATEX 		= pdflatex
BIBTEX		= bibtex
PREVIEW 	= open -a /Applications/Preview.app

GRAPHICS	= graphics
EPS_GFX  	= $(shell echo $(GRAPHICS)/*.eps)
GEN_GFX 	= $(addsuffix .pdf, $(basename $(EPS_FIGS)))

TEX_FILES	= $(shell find . -name '*.tex') $(shell find . -name '*.cls')
BIB_FILES	= $(shell find . -name '*.bib') $(shell find . -name '*.bst')
GFX_FILES	= #$(GEN_GFX)

DEP_FILES	= $(TEX_FILES) $(BIB_FILES) $(GFX_FILES)


all: $(PAPER).pdf

$(PAPER).pdf: $(DEP_FILES)
	$(LATEX) $(PAPER)
	$(BIBTEX) $(PAPER)
	$(LATEX) $(PAPER)
	$(LATEX) $(PAPER)

view: $(PAPER).pdf
	$(PREVIEW) $(PAPER).pdf

tidy:
	$(RM) $(PAPER).aux
	$(RM) $(PAPER).log
	$(RM) $(PAPER).bbl
	$(RM) $(PAPER).blg
	$(RM) $(PAPER).upa
	$(RM) $(PAPER).upb
	$(RM) $(PAPER).out

clean: tidy
	$(RM) $(PAPER).pdf

very_clean: clean
	$(RM) $(GEN_FIGS)
	
extract: $(PAPER).pdf
	pdftk $(PAPER).pdf cat 1 output $(SUMMARY).pdf
	pdftk $(PAPER).pdf cat 2-16 output $(DESCRIPTION).pdf
	pdftk $(PAPER).pdf cat 17-19 output $(REFERENCES).pdf
	pdftk $(PAPER).pdf cat 20 output $(PERSONNEL).pdf
	pdftk $(PAPER).pdf cat 21 output $(BUDGET).pdf
	pdftk $(PAPER).pdf cat 22 output $(FACILITIES).pdf
	pdftk $(PAPER).pdf cat 23 output $(DATA).pdf

%.pdf: %.eps
	epstopdf --outfile=$@ $<
