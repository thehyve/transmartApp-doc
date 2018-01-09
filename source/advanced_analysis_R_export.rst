Advanced Analysis Raw R Exports
===============================

-  `Boxplot`_
-  `Heatmap`_
-  `Linegraph`_
-  `Logistic regression`_
-  `Survival analysis`_
-  `Waterfall`_
-  `aCGH Frequency plot`_
-  `aCGH Survival analysis`_
-  `aCGH group test`_
-  `RNASeq group test`_

Boxplot
~~~~~~~
Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- ANOVA PAIRWISE file(s)
- ANOVA RESULTS file(s)
- Boxplot image file(s)

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an
overview of the input data for the analysis. At Parameters it shows the jobType to indicate the type of analysis and which image will be produced. The selected variables are displayed using the full concept path names for each of them.

In case of high-dimensional data this file contains information on which genes were selected for the independent and dependent variable names.

**Variables selected:**    
The items dependentVariable and independentVariable show the full path name of the items selected in tranSMART to use as input, reflect the two input box names in the user interface. Combining several items gives information on the type of variable selected and if the variable was used for binning or not. variablesConceptPaths gives a summary of all used concept paths.

divIndependentVariableType and divDependentVariableType indicate the type of
variables that were used. Values include CLINICAL for categorical and numeric
low-dimensional data types or the type of high-dimensional data that
was used, for example “mrna” incase of a mrna expression dataset.

dependentVariableCategorical and independentVariableCategorical indicate whether the selected variables are CATEGORICAL or not. Note the the X column in the outputfile.txt is either the CATEGORICAL variable or the binned variable (effectively turning it into a categorical variable).

div(In)dependetPathwayName gives the name of the genes in case of a high dimensional variable. 

flipImage is either True, when the Dependent variable is used to group the observations, or False, in case the Independent variable is used for grouping.

**Binning:**   
There are three different options for binning:

- EDP; Evenly Distribute Population
- ESB; Evenly Spaced Bins
- Manual binning

In case of EDP or ESB  for numerical or high-dimensional variables, the file will contain the following parameters to provide information on which variable was used to bin:

- binning; Either True or False
- binDistribution; EDP or ESB
- numberOfBins; Number of bins defined by the algorithm
- binVariable; either IND or DEP which stands for Independent or Dependent, respectively. Note that you can see which variable was used as independent or dependent using the independentVariable and dependentVariable items.

Information on the actual bin boundaries is available from the outputfile.txt in the column named X.

In case of the Manual binning option the above items are also included in the jobInfo but the item manualBinning will be set to True instead of False, indicating that manual bins were defined. Additionally, an item named binRanges is added to reflect the different bins manually defined. Note that both the numberOfBins and binVariable are still relevant in this case, while binDistribution is not.

outputfile.txt
++++++++++++++
The data with three to five columns describing the points plotted:

- PATIENT_NUM; Subject identifier
- X; The variable that is used to group the observations; categorical or binned. Can both be the independent or dependent variable depending on the data input.
- Y; The numerical variable used to plot the box. Can both be independent or dependent variable depending on the data input.
	
Optional columns when using multiple independent or/and dependent variables and when using high dimensional data:
  
- GROUP; Assigned automatically, name of either the independent or dependent group to be displayed in the boxplot
- GROUP.1; Assigned automatically, name of either the independent or dependent group to be displayed in the boxplot. Only used when GROUP is already present.

*NOTE:* Using two numerical or high-dimensional concepts requires binning of either the independent or the dependent variable.

When using high-dimensional data, it is possible to select multiple independent or dependent variables by selecting multiple genes or selecting a gene with multiple probes in the high dimensional pop-up. When a high-dimensional data point is binned, it will be treated as a category and will produce boxes determined by the bins. In case of plotting probe-level data, when for a selected gene more than one probe is available, this will result in one plot per probe.

When using two independent variables with two dependent variables this will produce a plot with two sets of boxes, each set will have two boxes, one for each dependent variable selected. In case of high-dimensional data each probe counts as a dependent variable producing its own box.

In case of using two high-dimensional concepts the GROUP and GROUP.1 names represent the probe names as stored in tranSMART. To find the gene names corresponding to the probes used, the two GROUP columns need to be combined with jobInfo.txt to see what was used as input for the X & Y columns. As mentioned before the X always represents the categorical or binned variable, to see whether to independent or dependent variable is used as X look at the “independentVariableCategorical” in jobInfo.txt. If it states False then the X is the dependent variable and if it is True the X is the dependent variable. The independent gene name is displayed next to the “divIndependentPathwayName” item and the dependent gene name is displayed next to the “divDependentPathwayName” item.

request.json
++++++++++++
json representation of the jobInfo.txt

ANOVA PAIRWISE file(s)
++++++++++++++++++++++
A contingency table view of the paired t-test p-values for each group. The file starts with the group name and then shows the contingency table for the variable selected to provide the numeric input.

In case two high-dimensional concepts were used as input, the output will consist of multiple files where the naming convention follows: ANOVA_PAIRWISE_<Gene/ProbeName>.txt. Note that the variable indicated as binning is used in the naming convention.

ANOVA RESULTS file(s)
+++++++++++++++++++++
A file with the ANOVA results for each group. Starts with the group name followed by a p-value overview for that group with both the p-value and F-statistic scores. Next a summary follows for each category showing one row per category option with the mean value and the number of instances in that category group.

If two high-dimensional concepts were used as input, the output will consist of multiple files where the naming convention follows: ANOVA_RESULTS_<Gene/ProbeName>.txt. Note that the binned variable is used in the naming convention.

Boxplot image file(s)
+++++++++++++++++++++
The boxplot stored as a PNG image file. When using two variables like genes with multiple probes taken from high-dimensional data, more than one image will be produced. Naming convention in that case is: BoxPlot_<ProbeName>.png

On the X-axis, the group names are displayed if the independent variable is chosen to be categorical. In case of multiple sets of boxes, the bars will be coloured and a legend will be provided to indicate which boxes correspond to which group. On the Y-axis, the numerical values are displayed when the dependent variable is chosen to be numeric. 

Note that switching around the independent and dependent variable will produce either a horizontal or vertical boxplot image.

Heatmap
~~~~~~~~
Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- Heatmap image file
- CMS.txt (Comparative Marker Selection, only for Marker selection)

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an overview of the input data for the analysis. At parameters it shows the jobType to indicate what analysis and image will be produced and it shows which variables were selected by displaying the full concept path names for each of them at indpendentVariable and variablesConceptPaths.

If applicable, the genes or proteins that were selected for the analysis are listed in the parameter divIndependentVariablePathwayName.

txtMaxDrawNumber shows the maximum number of rows to display and doGroupBySubject whether the box for ‘Group by subject (instead of node) for multiple nodes’ has been checked. calculateZscore and divIndependentVariableprobesAggregation show whether or not ‘Calculate z-score on the fly’ or probe aggregation were used, respectively.

outputfile.txt
++++++++++++++
The data with four columns describing the points plotted:

- PATIENT_NUM; 	The subject identifier with a prefix. The prefix is the subset identifier, indicated as either S1 or S2, followed by an underscore, the subject identifier, another underscore and the concept node name, e.g. ‘Genes’. Naming-conventions: <SUBSET_ID>_<PATIENT_ID>_<CONCEPT_NODE_NAME> or <SUBSET_ID>_<CONCEPT_NODE_NAME>_<PATIENT_ID>
- VALUE; The z-score for a patient for a probe
- GROUP; The probe name to which the value corresponds to
- GENE_SYMBOL;	The gene symbol the probe belongs to

The Markerselection analysis has two additional columns, instead of 'GROUP':

- PROBE.ID; The probe name of the platform
- SUBSET; Subset from which the patient sample originates.

request.json
++++++++++++
json representation of the jobInfo.txt

Heatmap.png
+++++++++++

The heatmap image with the rows depicting the gene or protein expression as :ref:`z-score<z-score-calculation-label>`. In 
case of multiple probes per gene/protein the expression per probe is shown, naming convention is <PROBENAME>_<GENENAME>. 
When probe aggregation was used, the gene (or protein) expression will be represented by the probe with the highest mean value for that particular gene/protein).

The default sorting of the heatmap is done by row, showing the row with the highest mean value first. By default the heatmap shows the first 50 probes. 
Each column shows the expression profile for a patient. The colours depict the :ref:`z-score<z-score-calculation-label>` intensity calculated during upload, 
unless the ‘calculate probe on the fly’-option was used. When two subsets were used, a yellow and orange bar indicates the two subsets. The 
same is true for Hierarchical Clustering and Marker Selection.

The jobInfo.txt can be used to determine which analysis was done and depending on which type of analysis that was used the output image will changed.

The RHClust job refers to the hierarchical clustering and the image will be differently sorted compared to the regular heatmap (RHeatmap job), unless no clustering options have been selected in the clustering analysis. Additionally, there is a dendrogram depicted on both the columns and the rows.

The RKClust job refers to the K-means clustering method. This analysis ignores subsets selected and aims to create subsets based on the z-scores found in the data. The image has grey and brown bars, indicating the different clusters.

All information on parameter selection can be found in the jobInfo.txt.

Column names naming-convention: <SUBSET_ID>_<CONCEPT_NODE_NAME>_<PATIENT_ID> or SUBSET_ID>_<PATIENT_ID>_<CONCEPT_NODE_NAME>. Row names naming-convention: <PROBE_ID>_<GENE_SYMBOL>

Specific to the MarkerSelection job, a CMS.txt (Comparative Marker Selection) will be generated.

CMS.txt
+++++++

The CMS.txt or, Comparative Marker Selection file, shows a seven column table, with default the top 50 markers that have differential probe/gene/protein expression. From left to right these columns are;

- GENE_SYMBOL; HGNC gene symbol
- PROBE.ID; probe identifier, can be a gene or protein name but could also be a reference to a gene or protein.
- logFC; log2 fold change
- t
- P.value
- adj.P.val; adjusted p-value
- B

**Note:** The adjusted p-value might not always provide the expected output and be the same for all genes.

For more information on these fields or how they are calculated please see the MarkerSelection analysis documentation :ref:`marker-selection-label`.

Linegraph
~~~~~~~~~

Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- LineGraph.png

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an
overview of the input data for the analysis. At parameters, it shows the jobType to indicate what analysis and image will be produced and it shows which variables were selected by displaying the full concept path names for each of them.

The selected graph type is indicated in the jobInfo.txt:

- MERR: Mean with error bar
- MSTD: Mean with standard deviation
- MEDER: Median with error bar
- IND: Plot individuals

**Variables selected:**
The items dependentVariable and groupByVariable show the full path name of the items selected in tranSMART to use as input. The independent and group by variable reflect the two input box names in the user interface: independent and outcome, respectively. Combining several items gives information on the type of variable selected and if the variable was used for binning or not.

divDependentVariableType and divGroupByVariableType indicate the type of variables that were used. Values include CLINICAL for categorical and numeric low-dimensional data types or the type of high-dimensional data that was used, for example “mrna” incase of a mrna expression dataset.

The dependent variable is always a numerical or high dimensional data node. The groupByVariable is always a categorical or binned variable.

**Binning:**
There are three different options for binning shown in binDistributionGroupBy:

- EDP; Evenly Distribute Population
- ESB; Evenly Spaced Bins
- Manual binning

In case of EDP or ESB for numerical or high-dimensional variables, the file will contain the following parameters to provide information on which variable was used to bin:

- binningGroupBy; Either True or False
- numberOfBinsGroupBy; Number of bins defined by the algorithm

In case of the Manual binning option the above items are also included in the jobInfo but the item manualBinningGroupBy will be set to True instead of False, indicating that manual bins were defined. Additionally, an item named binRangesGroupBy is added to reflect the different bins manually defined. Note that both the numberOfBins and binVariable are still relevant in this case, while binDistributionGroupBy is not.

outputfile.txt
++++++++++++++
The data with five columns describing the points plotted:

- PATIENT_NUM; Subject identifier
- VALUE; The value that is either being plotted or used to calculate the mean or median to plot
- GROUP; the variable name/path, this is indicated as dependent variable in the jobInfo.txt
- PLOT_GROUP; In case of high dimensional data contains probe, gene or protein name depending on the data selected. Otherwise will be empty.
- GROUP_VAR; The name of the (binned) group that a point belongs to.

request.json
++++++++++++
json representation of the jobInfo.txt

LineGraph.png
+++++++++++++

Image of plot. On the X-axis the time points are plotted. Each time point corresponds to a variable selected in the Time/Measurement Concepts-box. On the Y-axis the measurement is plotted, in parentheses the values that are being displayed (i.e. mean + se etc.). On the right there is a legend indicating which colour corresponds to each group.

Logistic regression
~~~~~~~~~~~~~~~~~~~

Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- LOGREG_RESULTS.txt
- LOGREGSummary.txt
- LogisticRegression.png

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an overview of the input data for the analysis. At parameters, it shows the jobType to indicate what analysis and image will be produced and it shows which variables were selected by displaying the full concept path names for each of them.

In case of high-dimensional data, this file contains information on which genes were selected for the analysis. If binning of high-dimensional data was done for the group variable, this will be indicated in this file. 

**Variables selected:**
The items independentVariable and groupByVariable show the full path name of the items selected in tranSMART to use as input. The independent and group by variable reflect the two input box names in the user interface: independent and outcome, respectively. Combining several items gives information on the type of variable selected and if the group variable was binned or not. variablesConceptPaths gives a summary of all used concept paths.

divIndependentVariableType and divGroupByVariable indicate the type of variables that were used. Values include CLINICAL for categorical and numeric low-dimensional data types or the type of high-dimensional data that was used, for example “mrna” incase of a mrna expression dataset. The independent variable is always a numerical or high dimensional data node. The groupByVariable is always a categorical or binned variable.

**Binning:**
There are three different options for binning:

- EDP; Evenly Distribute Population
- ESB; Evenly Spaced Bins
- Manual binning

In case of EDP or ESB for numerical or high-dimensional variables, the file will contain the following parameters to provide information on which variable was used to bin:

- binning; Either True or False
- numberOfBins; Number of bins defined by the algorithm
- binDistribution; EDP or ESB
- binVariable; IND, which stands for independent variable. Note that for logistic regression this is incorrectly displayed and the groupByVariable is the item that is always used for binning.

Information on the actual bin boundaries is available from the outputfile.txt in the column named X.

In case of the Manual binning option the above items are also included in the jobInfo but the item manualBinning will be set to True instead of False, indicating that manual bins were defined. Additionally, an item named binRanges is added to reflect the different bins manually defined. Note that both the numberOfBins and binVariable are still relevant in this case, while binDistribution is not.

outputfile.txt
++++++++++++++
The data with four columns describing the input data:

- PATIENT_NUM; Subject identifier
- X; the outcome variable options, in case of numerical binned variable this indicates the bin boundaries. Maximum of two groups possible in this analysis. This column is plotted on the Y-axis
- Y; the independent variable options, must be numerical or high dimensional concepts. This column is plotted on the X-axis
	
Optional columns when using multiple independent variables are GROUP and GROUP.1 (only possible when using high dimensional data with multiple probes per gene/protein or when selecting multiple genes/proteins). Depending on the type of data that was used as input, the GROUP can refer to either the X or the Y column.

- In case of high dimensional data for only the outcome variable the GROUP displays probe, gene or protein names for X.
- In case of high dimensional data for only the independent variable  the GROUP column displays probe, gene or protein names for Y.
- In case of a high dimensional node for both, GROUP refers to X and GROUP.1 refers to Y, showing probe, gene or protein names for Y.

request.json
++++++++++++
json representation of the jobInfo.txt

LOGREG_RESULTS.txt
++++++++++++++++++
A text file with the results of the general linear models(glm) algorithm in R. The I stands for the intercept and Y is the name of the independent variable input.
For more information on the glm function used in R please go `here <https://www.statmethods.net/advstats/glm.html>`__

LOGREGSummary.txt
+++++++++++++++++
A text file with the summary of the glm algorithme in R. The call used to model the data using glm is shown. In the coefficients table the Y represents the independent variables used as input.

LogisticRegression.png
++++++++++++++++++++++
An image file with two plots. The first plot shows the estimator over all the values inputted in the independent variable. The second plot is a ROC curve indicating the quality of the model with the AUC score.

Survival analysis
~~~~~~~~~~~~~~~~~

Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- CoxRegression_result.txt file(s)
- SurvivalCurve_FitSummary.txt file(s)
- SurvivalCurve_Table.txt file(s)
- SurvivalCurve.png file(s)

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an overview of the input data for the analysis. At parameters it shows the jobType to indicate the type of analysis and which image will be produced. The selected variables are displayed using the full concept path names for each of them.

In case of high-dimensional data this file contains information on which genes were selected for the independent and dependent variable names.

**Variables selected:**
timeVariable, categoryVariable and censoringVariable give an overview of the variables selected for the Time, Category and Censoring input boxes in the user interface. variablesConceptPaths gives a summary of all used concept paths.

divDependentVariableType indicates the type of variables that were used for the Category. Values include CLINICAL for categorical and numeric low-dimensional data types or the type of high-dimensional data that was used, for example “mrna” in case of a mrna expression dataset.

**Binning:**
There are three different options for binning:

- EDP; Evenly Distribute Population
- ESB; Evenly Spaced Bins
- Manual binning

In case of EDP or ESB for numerical or high-dimensional variables, the file will contain the following parameters to provide information on which variable was used to bin:

- binning; Either True or False
- binDistribution; EDP or ESB
- numberOfBins; Number of bins defined by the algorithm

Information on the actual bin boundaries is available in the outputfile.txt in the column named CATEGORY.

In case of the Manual binning option the abovementioned items are also included in the jobInfo but the item manualBinning will be set to True instead of False, indicating that manual bins were defined. Additionally, an item named binRanges is added to reflect the different bins manually defined. Note that both the numberOfBins and binVariable are still relevant in this case, while binDistribution is not.

The result_instance_id1 and 2 fields indicate the internal number tranSMART assigned to the subsets of patients. **NOTE:** The survival analysis groups subsets into one group and produces one survival plot based on the combined group.

outputfile.txt
++++++++++++++
The data with four columns describing the input data:

- PATIENT_NUM; Subject identifier
- TIME;	Values indicating the time someone survived, the unit (days, weeks) is dependent on the values loaded in tranSMART.
- CENSOR; Integer, values 0 or 1. 0 means a row is not censored, 1 means the row is used as a censored row during the analysis
- CATEGORY; The category/group, used to plot survival for the patients. In case of manual binning, the bin number is mentioned here. The bin contents can be found in the jobInfo.txt in this case.

Optional:

- GROUP; Only when using high-dimensional data to group variables. Indicates to which gene or probe the row of data belongs.

request.json
++++++++++++
json representation of the jobInfo.txt

CoxRegression_result.txt
++++++++++++++++++++++++
A text file with the results of the Cox regression analysis. Explains how tied events are handled, i.e. 
events with exactly the same survival time. For a full description on how the ties are handled 
please look `here <https://cran.r-project.org/web/packages/survival/survival.pdf>`__ under sections coxph and Surv.

Under 'Call:' the actual R command used to run the Cox regression is shown. Next two tables are displayed with the output coefficients:

- coef; Estimated coefficient from the linear model, β.
- exp(coef); Hazard ratio
- se(coef); Standard error
- z; z-score
- PR(>|z); The probability the estimated β could be 0.
- exp(-coef); 1/exp(coef), inverse hazard ratio
- lower .95; lower 95% confidence interval
- upper .95; upper 95% confidence interval

The last table in the file displays the Rsquare, Likelihood ratio test output, Wald test score and the Score (logrank) test output.

When using a high-dimensional concept to indicate the groups, this will produce one output file per gene or probe name. Naming convention: CoxRegression_result_<GENE_NAME>.txt or CoxRegression_result_<PROBE_NAME>.txt

For more information on the Cox regression analysis go `here <https://www.rdocumentation.org/packages/survival/versions/2.41-2/topics/coxph>`__.

SurvivalCurve_FitSummary.txt
++++++++++++++++++++++++++++
A text file that shows the summary for the survfit analysis in R.

Under 'Call:' the actual R command used to run the survfit is shown. The table below in the file displays for each plotted category: 

- n; number of subjects 
- events; number of events 
- median; median time value 
- 0.95 LCL; lower range of time variable, 95% confidence interval 
- 0.95 UCL; upper range of time variable, 95% confidence interval 

When using a high-dimensional concept to indicate the groups this will produce
one output file per gene or probe name.

Naming convention: SurvivalCurve_<GENE_NAME>_FitSummary.txt or SurvivalCurve_<PROBE_NAME>_FitSummary.txt

For more information on the survfit function go `here <https://www.rdocumentation.org/packages/survival/versions/2.11-4/topics/survfit>`__.

SurvivalCurve_Table.txt
+++++++++++++++++++++++
A text file that shows the table for the survfit analysis in R.

When using a high-dimensional concept to indicate the groups this will produce one output file per gene or probe name. Naming convention: SurvivalCurve_<GENE_NAME>_Table.txt or SurvivalCurve_<PROBE_NAME>_Table.txt

Under 'Call:' the actual R command used to run the survfit is shown. The table in this file has the following columns per category:

- time; time of event
- n.risk; number of subjects for whom the event did not (yet) occur
- n.event; number of subjects for which the event occurred at that specific time
- survival; percentage of subjects not (yet) affected by the event
- std.err; standard error
- lower 95% CI; lower 95% confidence interval
- upper 95% CI; upper 95% confidence interval

For more information on the survfit function go `here <http://stat.ethz.ch/R-manual/R-devel/library/survival/html/summary.survfit.html>`__.

SurvivalCurve.png
+++++++++++++++++
The Kaplan-Meier plot to display the results of the survival analysis. On the X-axis the time line and on the Y-axis the fraction of patients.
The unit of time depends on the unit loaded into tranSMART. The legend indicates which group corresponds to what colour.

When using a high-dimensional concept to indicate the groups, this will produce one output file per gene or probe name. 
Naming convention: SurvivalCurve_<GENE_NAME>.png or SurvivalCurve_<PROBE_NAME>.png

Waterfall
~~~~~~~~~
Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- Waterfall image file

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an overview of the input data for the analysis. At parameters, it shows the jobType to indicate the type of analysis and which image will be produced. The selected variable is displayed using the full concept path name next to dataNode and variablesConceptPaths. The parameters highRangeValue and lowRangeValue indicate the user set boundaries during the parameter selection. Thresholds that are set are either exclusive or inclusive dependent on the chosen operator signs found at lowRangeOperator and highRangeOperator.

outputfile.txt
++++++++++++++
The data with three columns describing the points plotted:

- PATIENT_NUM; Subjectt identifier
- X; the value of the selected variable
- GROUP; Assigned automatically, either HIGH, LOW or BASE. Dependent on user set boundaries. The HIGH and LOW group are subjects/patients for which the numerical value is above or below the set thresholds, respectively.				

request.json
++++++++++++
json representation of the jobInfo.txt

Waterfall.png
+++++++++++++
The waterfall plot stored as a PNG image file. A sorted bar plot with the lowest value on the left and the highest value on the right. Default colour for LOW is red, for HIGH is blue and for BASE is black. If one of the categories is missing from the data due to thresholds selected, the color of the LOW and HIGH groups are shifted to black and red, respectively, instead of red and blue. If all values fall within one category all of the bars will be black. Each bar represents one patient or subject.

aCGH Frequency plot
~~~~~~~~~~~~~~~~~~~
Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- phenodata.tsv
- frequency-plot.png

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an overview of the input data for the analysis. At parameters it shows the jobType to indicate the type of analysis and which image will be produced. The selected variables are displayed using the full concept path names for each of them.

**Variables selected:**
groupVariable and regionVariable show the concept paths of the variables used for grouping and the aCGH region, respectively. variablesConceptPaths gives a summary of all used concept paths.

outputfile.txt
++++++++++++++
This file contains the data that was used to do the analysis. Depending on what was uploaded to tranSMART, not all columns might contain data.

The first five columns describe the region itself. Indicating the chromosome it is on, the base pair start and end position, number of probes present in the region and the cytoband(s) it covers.

All columns thereafter are sample-specific. The prefix of each column describes what kind of data it contains:

- chip; Log2 ratio of the measurement
- flag; Copy number state of the region. -2 (homozygous loss), -1 (loss) 0, (normal), 1 (gain), 2 (amplification)
- probhomloss; Probability of homozygous loss
- probloss; Probability of loss  
- probnorm; Probability of normal
- probgain; Probability of gain
- probamp; Probability of amplification

*Note:* when opening the file as a spreadsheet, the header is shifted one column to the right of its corresponding data values.


request.json
++++++++++++
json representation of the jobInfo.txt

phenodata.tsv
+++++++++++++
A file with two columns: PATIENT_NUM and GROUP. The PATIENT_NUM shows the subject identifiers and the group column describes to which group each subject belongs.

frequency-plot.png
++++++++++++++++++
An image file with one plot per group. Depending on the selected input data either produces a simple frequency plot or a frequency plot using `qDNAseq <http://bioconductor.org/packages/release/bioc/manuals/QDNAseq/man/QDNAseq.pdf>`_. The simple frequency plot is used when there is overlap in the regions/genes selected, when there is no overlapping data the qDNAseq plotting is used.

Simple frequency plot:

- X-axis shows the chromosomes where the size of the chromosomes is determined by the number of probes used to measure the data. The X-axis label indicates that it shows the “chromosome (number of probes)”.
- The left-hand Y-axis shows the frequency of gains and losses, the right-hand side shows the False Discovery Rate (FDR) which is not plotted.

qDNAseq plot:

- The X-axis shows chromosomes where the size of the chromosomes are determined by the number of base pairs in the chromosomes. The X-axis label indicates that is shows “chromosome (base pairs)”.
- The Y-axis shows the frequency of gains and losses.
- In the top left corner the number of bins and used bin size in kilo basepairs (kbp) are displayed.
- In the top right corner the number of samples for which the data was plotted is shown.

aCGH Survival analysis
~~~~~~~~~~~~~~~~~~~~~~

Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- phenodata.tsv
- survival-test.txt
- aCGHSurvivalAnalysis_<chr>_<region>.png files

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an overview of the input data for the analysis. At parameters it shows the jobType to indicate the type of analysis and which image will be Produced. The selected variables are displayed using the full concept path names for each of them.

The Alteration Type of the analysis is shown in the aberrationType parameter, which will be either -1 (LOSS vs NO LOSS), 0 (LOSS vs NORMAL vs GAIN) or 1 (GAIN vs NO GAIN). numberOfPermutations shows the total permutations performed.

**Variables selected:**
timeVariable and regionVariable show the concept paths of the variables used for survival time and the aCGH region, respectively. variablesConceptPaths gives a summary of all used concept paths.

outputfile.txt
++++++++++++++
This file contains the data that was used to do the analysis. Depending on what was uploaded to tranSMART, not all columns might contain data.

The first five columns describe the region itself. Indicating the chromosome it is on, the base pair start and end position, number of probes present in the region and the cytoband(s) it covers.

All columns thereafter are sample-specific. The prefix of each column describes what kind of data it contains:

- chip; Log2 ratio of the measurement
- flag; Copy number state of the region. -2 (homozygous loss), -1 (loss) 0, (normal), 1 (gain), 2 (amplification)
- probhomloss; Probability of homozygous loss
- probloss; Probability of loss  
- probnorm; Probability of normal
- probgain; Probability of gain
- probamp; Probability of amplification

*Note:* when opening the file as a spreadsheet, the header is shifted one column to the right of its corresponding data values.

request.json
++++++++++++
json representation of the jobInfo.txt

phenodata.tsv
+++++++++++++
This file reflects all subjects in the selected subset, which have data for the survival time concept. Some of these patients might not have data for the selected aCGH concept. These patients will not be taken into account for the analysis.

- PATIENT_NUM; Subject identifier
- TIME; Values indicating the survival time. The unit (days, weeks, months) is dependent on the values loaded in tranSMART.
- CENSOR; Integer, values 0 or 1. 0 means a row is not censored, 1 means the row is censored in the analysis.

survival-test.txt
+++++++++++++++++
The survival-test.txt file contains for the most part the same data as the outputfile.txt, but with two columns added showing the result of the permutation test. For each region the p-value column shows the significance of the survival differences between the defined groups, whereas FDR represents the false discovery rate.

*Note:* when opening the file as a spreadsheet, the header is shifted one column to the right of its corresponding data values.

aCGHSurvivalAnalysis_<chr>_<region>.png
+++++++++++++++++++++++++++++++++++++++
The Kaplan–Meier curve for each region is stored as a PNG image file. Depending on the alteration type chosen, there will be either two (for GAIN vs NO GAIN or LOSS vs NO LOSS) or three (for LOSS vs NORMAL) groups shown which are described in the legend on the bottom-left. The X-axis shows the Survival Time parameter, whereas the survival proportion is on the Y-axis.

P-value, False Discovery Rate (FDR) and the region name are shown on the bottom-right.

aCGH group test
~~~~~~~~~~~~~~~

Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- phenodata.tsv
- groups-test.txt
- groups-test.png

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an overview of the input data for the analysis. At parameters it shows the jobType to indicate the type of analysis and which image will be produced. The selected variables are displayed using the full concept path names for each of them.

The Alteration Type of the analysis is shown in the aberrationType parameter, which will be either -1 (LOSS), 0 (BOTH) or 1 (GAIN). numberOfPermutations shows the total permutations performed, while statisticsType indicates the test chosen in the Statistical Test option (Chi-square, Wilcoxon or Kruskal-Wallis).

**Variables selected:**
groupVariable and regionVariable show the concept paths of the variables used for grouping and the aCGH region variable, respectively. variablesConceptPaths gives a summary of all used concept paths.

outputfile.txt
++++++++++++++
This file contains the data that was used to do the analysis. Depending on what was uploaded to tranSMART, not all columns might contain data.

The first five columns describe the region itself. Indicating the chromosome it is on, the base pair start and end position, number of probes present in the region and the cytoband(s) it covers.

All columns thereafter are sample-specific. The prefix of each column describes what kind of data it contains:

- chip; Log2 ratio of the measurement
- flag; Copy number state of the region: -2 (homozygous loss), -1 (loss) 0, (normal), 1 (gain), 2 (amplification)
- probhomloss; Probability of homozygous loss
- probloss; Probability of loss
- probnorm; Probability of normal
- probgain; Probability of gain
- probamp; Probability of amplification

**Note:** when opening the file as a spreadsheet, the header is shifted one column to the right of its corresponding data values.

request.json
++++++++++++
json representation of the jobInfo.txt

phenodata.tsv
+++++++++++++
This file reflects all subjects in the selected subset, which have data for the group concept. Some of these patients might not 
have data for the selected aCGH concept. These patients will not be taken into account for the analysis.

- PATIENT_NUM; Subject identifier
- Group; Which of the selected groups the patient belongs to
    
group-test.txt
++++++++++++++
The groups-test.txt file contains the same general information about the regions as the outputfile.txt, but instead of sample-specific values it shows the gain/loss frequencies (proportions) for each group used in the analysis.

For each region the p-value column shows the significance of the differences in gain/loss frequency between the groups defined. The FDR column represents the false discovery rate.

group-test.png
++++++++++++++
The groups-test.png file shows a frequency plot of the chromosomal gains and/or losses for two groups used in the analysis. *Note:* when there are more than two groups selected, only the first two are shown. If Alteration Type "BOTH" was chosen in the analysis, the gains and losses will be shown in two separate graphs. 

Which two groups are being compared is shown on the far left side of the plot on the bottom and top corner. The X-axis shows the chromosomes. On the left Y-axis, the percentage of affected subjects in the group is shown (blue for gains, red for losses). The black line represents the False Discovery Rate (FDR), for which the proportion is shown on the right Y-axis.

RNASeq group test
~~~~~~~~~~~~~~~~~

Files included in export:

- jobInfo.txt
- outputfile.txt
- request.json
- phenodata.tsv
- rawreadcount.txt
- normalizedreadcount.txt
- probability.txt
- rnaseq-groups-test.png

jobInfo.txt
+++++++++++
The job information submitted to tranSMART. The job information gives an overview of the input data for the analysis. At parameters it shows the jobType to indicate the type of analysis and which image will be produced. The selected variables are displayed using the full concept path names for each of them.

The analysisType parameter shows whether a two group unpaired or multi-group analysis was performed.

**Variables selected:**
groupVariable and RNASeqVariable show the concept paths of the variables used for grouping and the RNAseq variable, respectively. variablesConceptPaths gives a summary of all used concept paths.

outputfile.txt
++++++++++++++
This file contains the data that was used to do the analysis. Depending on what was uploaded to tranSMART, not all columns might contain data.

The first six columns describe the region itself. Indicating the chromosome it is on, the base pair start and end position, number of probes present in the region, the cytoband(s) it covers and the HGNC gene symbol.

All columns thereafter are sample-specific. For each sample a column with the read counts for all regions/genes is shown.

*Note:* when opening the file as a spreadsheet, the header is shifted one column to the right of its corresponding data values.

request.json
++++++++++++
json representation of the jobInfo.txt

phenodata.tsv
+++++++++++++
This file reflects all subjects in the selected subset, i.e. that are present in one of the groups defined. Some of these patients 
might not have data for the selected RNA-Seq concept. These patients will not be taken into account for the analysis.
    
- PATIENT_NUM; Subject identifier
- Group; Which of the selected groups the patient belongs to

rawreadcount.txt
++++++++++++++++
Table that contains the raw read counts for all the patients that were used in the group-test analysis.

*Note:* when opening the file as a spreadsheet, the header is shifted one column to the right of its corresponding data values.

normalizedreadcount.txt
+++++++++++++++++++++++
Table that contains the normalized, log-transformed read counts for all the patients that were used in the group-test analysis.

*Note:* when opening the file as a spreadsheet, the header is shifted one column to the right of its corresponding data values.

probability.txt
+++++++++++++++
This file contains the results of the group-test analysis for each Region name/gene symbol:

- logFC; Log2 fold change between the groups
- logCPM; Log-Concentration count-per-million
- Pvalue; The significance of the read count difference between the groups
- FDR; False discovery rate

rnaseq-groups-test.png
++++++++++++++++++++++
The rnaseq-groups-test.png consists of three separate plots created with the Bioconductor R package:

MDS plot: a multi-dimensional scaling plot of the RNA samples in which distances correspond to leading log-fold-changes between each pair of RNA samples. The leading log-fold-change is the average (root-mean-square) of the largest absolute log-fold-changes between each pair of samples. Distances between samples correspond to leading biological coefficient of variation (BCV) between those samples. This plot can be viewed as a type of unsupervised clustering.

BCV plot: shows the root-estimate, i.e., the genewise biological coefficient of variation (BCV) against gene abundance (in log2 counts per million).

MA plot: Log-Fold Change (logFC) versus Log-Concentration count-per-million (logCPM).
