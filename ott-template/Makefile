.PHONY: ott-preview
ott-preview:
	ott system.ott -o system-ott.tex -tex_show_meta false \
  && { pdflatex -interaction=nonstopmode system-ott.tex \
    && open system-ott.pdf \
    || tail system-ott.log; } \
  && rm system-ott.tex system-ott.aux

quick: ott-preview
