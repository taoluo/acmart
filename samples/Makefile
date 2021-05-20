PACKAGE=acmart

timestamp: samples.dtx samples.ins acmart.cls acmart-tagging.sty ACM-Reference-Format.bst 
	pdflatex samples.ins
	for texfile in *.tex; do \
	pdffile=$${texfile%.tex}.pdf; \
		${MAKE} $$pdffile; \
	done
	touch timestamp

%.cls: ../%.cls
	ln -s $< .

%.sty: ../%.sty
	ln -s $< .

%.bst: ../%.bst
	ln -s $< .


%.pdf:  %.tex   $(PACKAGE).cls ACM-Reference-Format.bst 
	cd $(dir $@) && pdflatex-dev $<
	- cd $(dir $@) && bibtex $(basename $<)
	cd $(dir $@) && pdflatex-dev $<
	cd $(dir $@) && pdflatex-dev $<
	while ( grep -q '^LaTeX Warning: Label(s) may have changed' $(basename $<).log) \
	  do cd $(dir $@) && pdflatex-dev $<; done

sample-xelatex.pdf:  sample-xelatex.tex   $(PACKAGE).cls ACM-Reference-Format.bst 
	cd $(dir $@) && xelatex-dev $<
	- cd $(dir $@) && bibtex $(basename $<)
	cd $(dir $@) && xelatex-dev $<
	cd $(dir $@) && xelatex-dev $<
	while ( grep -q '^LaTeX Warning: Label(s) may have changed' $(basename $<).log) \
	  do cd $(dir $@) && xelatex-dev $<; done

sample-lualatex.pdf:  sample-lualatex.tex   $(PACKAGE).cls ACM-Reference-Format.bst 
	cd $(dir $@) && lualatex-dev $<
	- cd $(dir $@) && bibtex $(basename $<)
	cd $(dir $@) && lualatex-dev $<
	cd $(dir $@) && lualatex-dev $<
	while ( grep -q '^LaTeX Warning: Label(s) may have changed' $(basename $<).log) \
	  do cd $(dir $@) && lualatex-dev $<; done

#
#  The tagged code is experimental;  expect breaking...
#
sample-sigconf-tagged.pdf: sample-sigconf-tagged.tex   $(PACKAGE).cls ACM-Reference-Format.bst acmart-tagging.sty
	- cd $(dir $@) && pdflatex-dev -halt-on-error $<
	- cd $(dir $@) && bibtex $(basename $<)
	- cd $(dir $@) && pdflatex-dev -halt-on-error $<
	- cd $(dir $@) && pdflatex-dev -halt-on-error $<
	- while ( grep -q '^LaTeX Warning: Label(s) may have changed' $(basename $<).log) \
	  do cd $(dir $@) && pdflatex-dev -halt-on-error $<; done
