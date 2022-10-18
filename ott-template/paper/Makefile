OTT = ott
OTT_FLAGS := -tex_wrap false -tex_show_meta false -picky_multiple_parses false
PDF := paper.pdf

default: quick

quick : quick_aux

# List all files here that need to be otted
FILES := paper.tex \
	 main.tex \
	 other.tex


FILES-TARGETS := $(subst .tex,-ottput.tex,$(FILES))
FILTER := $(subst .tex,.tex ,$(addprefix -tex_filter ,$(join $(FILES),$(FILES-TARGETS))))

SYSTEM_OTT := ../system.ott

main-ottput.tex : main.tex $(SYSTEM_OTT)
	$(OTT) $(OTT_FLAGS) -i $(SYSTEM_OTT) -o system-ott.tex -tex_name_prefix SYSTEM \
		-tex_filter main.tex main-ottput.tex

paper-ottput.tex : paper.tex $(FILES) $(SYSTEM_OTT)
	$(OTT) $(OTT_FLAGS) -i $(SYSTEM_OTT) -tex_name_prefix SYSTEM $(FILTER)
	$(OTT) $(OTT_FLAGS) -i $(SYSTEM_OTT) -o system-ott.tex -tex_name_prefix SYSTEM \
		-tex_filter paper.tex paper-ottput.tex

quick_aux: paper-ottput.tex $(FILES) Makefile
	pdflatex -shell-escape -synctex=1 -file-line-error -interaction=nonstopmode -halt-on-error paper-ottput.tex
	mv paper-ottput.pdf paper.pdf


full: full_aux

full_aux: $(FILES) Makefile
	pdflatex -shell-escape -synctex=1 -file-line-error -interaction=nonstopmode -halt-on-error paper-ottput.tex \
	&& bibtex paper-ottput \
	&& pdflatex -shell-escape -synctex=1 -file-line-error -interaction=nonstopmode -halt-on-error paper-ottput.tex \
	&& pdflatex -shell-escape -synctex=1 -file-line-error -interaction=nonstopmode -halt-on-error paper-ottput.tex
	mv paper-ottput.pdf paper.pdf

aux: $(FILES) Makefile
	pdflatex -shell-escape -synctex=1 -file-line-error -interaction=nonstopmode -halt-on-error "\def\isaux{1}\input{paper.tex}"

clean :
	rm -f *.aux *.dvi *.ps *.log *-ott.tex *-ottput.tex *.bbl *.blg *.rel *~ *.vtc *.out *.spl *-inc.tex
