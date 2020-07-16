# Known suffixes.
.SUFFIXES: .aux .bbl .bib .blg .dvi .htm .html .css .log .out .pdf .ps .tex \
	.toc .foo .bar

# Master list of stems of tex files in the project.
# Should be the same as in the main Makefile
# except that it includes the bibliography
LIJST = introduction representationtheory representations-compact \
	liegroups-general liestructure vermamodules \
    algebraicgroups  galoiscohomology reductiveforms  \
	representations-local plancherel discreteseries \
    automorphicspace automorphicforms bibliography

# book is a special case
LIJST_TAGS = $(LIJST) fdl index

FOOS = $(patsubst %,%.foo,$(LIJST_TAGS))
BARS = $(patsubst %,%.bar,$(LIJST_TAGS))
PDFS = $(patsubst %,%.pdf,$(LIJST_TAGS))

PDFLATEX := ../latex.sh "pdflatex"

.PHONY: all
all: book.pdf $(PDFS)

# We need the following to cancel the built-in rule for
# dvi files (which uses tex not latex).
%.dvi : %.tex

# Make aux file
%.foo: %.tex
	$(PDFLATEX) $*
	$(PDFLATEX) $*
	touch $*.foo

# These do not get bibtexed
index.bar:
	touch index.bar

fdl.bar:
	touch fdl.bar

# Make bbl file
%.bar: %.foo
	bibtex $*
	touch $*.bar

# Make pdf file from others
%.pdf: %.tex %.bar $(FOOS)
	$(PDFLATEX) $*
	$(PDFLATEX) $*
