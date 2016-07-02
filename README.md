## AutoReportLite
Automatic analysis pipline &amp; reporting template, using bash, R, and LaTeX. 

### Analysis Pipeline Setup

#### Step 1. 
Create sample sheet to describe samples for analysis and other relevant information per sample (`sample-sheet.tsv`)

#### Step 2.
Setup analysis pipeline script using items from sample sheet (`code/analysis_pipeline.sh`)

#### Step 3.
Parse the sample sheet to create subdirectories per sample and pass items to the script for analysis (`workflow.Rmd`)

### Report Compilation

#### Step 4.
Adjust report file to set project information, file paths, figures, as needed for inclusion in the report (`report/auto-report.Rnw`). 

#### Step 5.
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
#### Step 6.
Compile the resulting TEX file with `pdflatex` 2 or 3 times (yes this is necessary!)

```
$ pdflatex auto-report.tex && pdflatex auto-report.tex && pdflatex auto-report.tex
```



#### TIPS:
- Use the workflow.Rmd to set up your pipeline's directory structure
- Create a parent directory for the pipeline output (e.g. `analysis_pipeline`), with a subdirectory for each sample to be processed (`Sample1`,`Sample2`,etc.); the name of the subdirectory should correspond to the name or ID for the sample
- Set up your pipeline script to work on one sample, and output all of that sample's results in its corresponding pipeline subdir
- If not using `qsub` for script submission then pipe the stdout and stderr from the pipeline script to log files
- If not using `qsub` then run the pipeline script in a `for` loop from the workflow.Rmd
- You can easily embed the code for your analysis pipeline directly into the report RNW file; I omit this here since my pipelines often require resources unavailable in this context, and you may run into problems with `qsub` job output dependencies and background processes.
