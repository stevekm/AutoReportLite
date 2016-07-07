### Report Compilation

#### Step 1.
Adjust report file to set project information, file paths, figures, as needed for inclusion in the report (in file`auto-report.Rnw`, file paths are in code chunk labeled `report_setup`). 

#### Step 2.
Compile the RNW file with knitr:

```
$ # in terminal, change to report dir and start R
$ cd report
$ R
> # if knitr is not installed, install it:
> # install.packages("knitr")
> # load knitr
> library("knitr")
> # 'knit' the file
> knit("auto-report.Rnw")
...
output file: auto-report.tex

[1] "auto-report.tex"
> # quit R and return to the terminal
> quit()
```
#### Step 3.
Compile the resulting TEX file with `pdflatex` 2 or 3 times for full compilation.

```
$ pdflatex auto-report.tex && pdflatex auto-report.tex && pdflatex auto-report.tex
```


