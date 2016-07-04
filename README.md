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
Adjust report file to set project information, file paths, figures, as needed for inclusion in the report (in file`report/auto-report.Rnw`, file paths are in code chunk labeled `report_setup`). 

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
Compile the resulting TEX file with `pdflatex` 2 or 3 times for full compilation.

```
$ pdflatex auto-report.tex && pdflatex auto-report.tex && pdflatex auto-report.tex
```



#### TIPS:
- Use the `workflow.Rmd` to set up your pipeline's directory structure
- Create a parent directory for the pipeline output (e.g. `analysis_pipeline`), with a subdirectory for each sample to be processed (`Sample1`,`Sample2`,etc.); the name of the subdirectory should correspond to the name or ID for the sample. See this example:

```
steve@macbook:~/AutoReportLite$ tree analysis_pipeline/
analysis_pipeline/
|-- Sample1
|   |-- R_stats.txt
|   |-- Sample1.distribution_histogram.pdf
|   |-- Sample1.random_distribution.pdf
|   `-- logs
|       |-- analysis_pipeline.sh.e4783069
|       |-- analysis_pipeline.sh.o4783069
|       |-- analysis_pipeline.sh.pe4783069
|       |-- analysis_pipeline.sh.po4783069
|       `-- scriptlog.analysis_pipeline.sh.20160429t173756.highmem001.61335.15519
|-- Sample2
|   |-- R_stats.txt
|   |-- Sample2.distribution_histogram.pdf
|   |-- Sample2.random_distribution.pdf
|   `-- logs
|       |-- analysis_pipeline.sh.e4783070
|       |-- analysis_pipeline.sh.o4783070
|       |-- analysis_pipeline.sh.pe4783070
|       |-- analysis_pipeline.sh.po4783070
|       `-- scriptlog.analysis_pipeline.sh.20160429t173756.highmem001.61390.15152

...

```

- Set up your pipeline script to work on one sample, and output all of that sample's results in its corresponding pipeline subdir
- If not using `qsub` for script submission then pipe the stdout and stderr from the pipeline script to log files
- If not using `qsub` then run the pipeline script in a `for` loop from the workflow.Rmd
- You can easily embed the code for your analysis pipeline directly into the report RNW file; I omit this here since my pipelines often require resources unavailable in this context, and you may run into problems with `qsub` job output dependencies and background processes.


---
### Dependencies

- R and the `knitr` package (I'm currently using R 3.3.0, but others may work)
- LaTeX and pdflatex (I'm currently using `pdfTeX 3.14159265-2.6-1.40.16 (TeX Live 2015)`, but others may work; I've also used this with `pdfTeX using libpoppler 3.141592-1.40.3-2.2 (Web2C 7.5.6)` (standard with CentOS 6), extra .sty files as needed are included with the report)
- bash (I'm currently using `GNU bash, version 4.1.2(1)-release (x86_64-redhat-linux-gnu)`, but others may work; on OS X `GNU bash, version 3.2.57(1)-release (x86_64-apple-darwin15)` works but note that some commands such as `readlink` are not available, some alternatives may be found in the `coreutils` package availble in `homebrew` e.g. `greadlink`, etc.)
- any software used by your specific pipelines
