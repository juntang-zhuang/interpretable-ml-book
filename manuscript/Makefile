all : html

book.file := Book.txt
md.files := $(shell cat ${book.file})

package: ../DESCRIPTION ../R/*.R
	Rscript  -e "devtools::install('../')"

html : *.Rmd
	# When build fails interpretable-ml.Rmd is created and not removed. Next build will fail when file exists.
	rm -f interpretable-ml.Rmd
	Rscript  -e "bookdown::render_book('./', 'bookdown::gitbook')"

leanpub : $(md.files)

%.md : %.Rmd
	Rscript  -e "knitr::knit('$<', envir = new.env())" 
	R --no-save --args $@ < fixmath.R


pdf : interpretable-ml.pdf

interpretable-ml.pdf : *.Rmd
	# When build fails interpretable-ml.Rmd is created and not removed. Next build will fail when file exists.
	rm -f interpretable-ml.Rmd
	Rscript  -e "bookdown::render_book('./', 'bookdown::pdf_book')"
	pdflatex $<
	
epub : _book/interpretable-ml.epub
	
_book/interpretable-ml.epub : *.Rmd
	# When build fails interpretable-ml.Rmd is created and not removed. Next build will fail when file exists.
	rm -f interpretable-ml.Rmd
	Rscript  -e "bookdown::render_book('./', 'bookdown::epub_book')"
	
	
mobi : _book/interpretable-ml.epub
	# When build fails interpretable-ml.Rmd is created and not removed. Next build will fail when file exists.
	rm -f interpretable-ml.Rmd
	Rscript  -e "bookdown::kindlegen('./_book/interpretable-ml.epub', exec = '../kindlegen')"

