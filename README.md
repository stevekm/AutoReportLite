# AutoReportLite
Automatic analysis pipline &amp; reporting template, using bash, R, and LaTeX. 

### Step 1. 
Create sample sheet to describe samples for analysis and other relevant information per sample (sample-sheet.tsv)

### Step 2.
Setup analysis pipeline script using items from sample sheet (code/analysis_pipeline.sh)

### Step 3.
Parse the sample sheet to create subdirectories per sample and pass items to the script for analysis (workflow.Rmd)

### Step 4.
Adjust report file to set project information, file paths, figures, as needed for inclusion in the report (auto-report.Rnw). Compile the report with knitr in R (.Rnw -> .tex) and pdflatex in the terminal (.tex -> .pdf)
