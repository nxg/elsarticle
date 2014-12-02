CHECKS=test-inproceedings test-eprints

%.bbl: %.aux model2-names-test.bib ../model2-names-astronomy.bst
	bibtex $<

%.diff: %.bbl
	rm -f $@
	diff ${<}-correct $< >$@ || :

# The following succeeds, and prints 'All tests OK', if all of the
# .diff files are of zero size; if one or more is non-empty, it
# reports that, and ends reporting an error.
#
# 'test -s filename' is true if 'filename' exists and has non-zero size
check: $(CHECKS:=.diff)
	@allgood=:; \
	  for f in $(CHECKS); do \
	    if test -s $$f.diff; then \
	      echo "FAIL: $$f"; allgood=false; \
	    else \
	      echo "OK: $$f"; rm $$f.diff; \
	    fi; \
	  done; \
	$$allgood
	@echo "All tests OK"

clean:
	rm -f *.bbl *.blg *.diff
