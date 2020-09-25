PAPER 		= Proposal

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

%.pdf: %.eps
	epstopdf --outfile=$@ $<
