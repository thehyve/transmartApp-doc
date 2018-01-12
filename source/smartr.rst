|smartr_main|

*Heatmap: a typical SmartR view* 

.. _smartr-label:

SmartR
======

Workflows provided by SmartR:

-   `Boxplot Workflow`_

-   `Correlation Workflow`_

-   `Heatmap Workflow`_

-   `Linegraph Workflow`_

-   `Volcanoplot Workflow`_


General
~~~~~~~

In addition to the :ref:`advanced-workflow-label` a more interactive mode of visualising 
data in tranSMART has been created. *SmartR* uses modern technologies to create interactive
graphs directly from within tranSMART. Although the technologies are different some of the 
functionalities are similar, this means a user will have multiple options for creating a
desired graph. Which is best depends on the type and volume of data to visualise.

How to run SmartR workflows
~~~~~~~~~~~~~~~~~~~~~~~~~~~

To begin to run any analysis:

#.  In **Analyze**, open the study of interest.

#.  Define the cohort(s) you want to analyze by dragging one or more
    concepts into empty subset definition boxes. For more information,
    see :ref:`defining-the-cohorts-label`.

    The following sections describe how to run specific analyses after you
    perform the above steps.

#.  Select a SmartR workflow from the main SmartR tab.

#.  Empty selection boxes appear that allow you to drag in numerical, categorical and high dimensional 
    nodes of interest. The boxes change colour based on whether suitable input is detected:

    |smartr_empty_selection|

    For most workflows you need to select specific markers from the high dimensional data set:

    |smartr_selection_highdim|
    
#.  Click **Fetch data**. This will transport the data from tranSMART into the SmartR computational *R* environment.
    Once ready, SmartR will provide summaries of the retrieved data.
    
    |smartr_fetch_summaries|

#.  (Optional) The pre-processing tab allows you to perform modifications to your data if this is necessary.
    For instance, this could be recalculating *z-scores* based on current selection criteria, or performing
    *probe aggregation*.

#.  Use your data in SmartR analyses by clicking **Run Analysis**. The page you see there is unique
    to the workflow you have chosen.

.. important::
    If you want to rerun a workflow after changing the source data, you **always** have to click **Fetch data** again.

General Functionality
~~~~~~~~~~~~~~~~~~~~~

The following functionalities are available in multiple workflows:

-   **Capture SVG**: this button allows you to download the current image to your local computer. Note: this
    does not always work as well as expected.

Boxplot Workflow
~~~~~~~~~~~~~~~~

After fetching data the Boxplot workflow will draw a box and whiskers plot for every numerical node or gene
selected in the previous step. Using the mouse you can zoom in to specific parts of the graphs.
Also visible in the workflow are:

-   Controls to select data transformations: *raw*, *log2*, or *log10* transformed.

-   A legend that shows the colours for selected nodes.
-   Controls to change or reset the current view on the data or to download the current image.
-   Also, the plot title shows the result of a calculated ANOVA test for the selected variables.

|smartr_boxplot|

In each graph in the plot the following is shown:

-   Dots with the value for each individual.
-   A box that indicates the median and *interquartile range*, details are shown when you hover-over the graph.
-   Whiskers that extend up- and downward 1.5 * the IQR.
-   A diamond that indicates the mean and confidence level. 

.. note::
    
    When zoomed in, you can reset the view by clicking the specific icon in the plot control bar.

Correlation Workflow
~~~~~~~~~~~~~~~~~~~~

After fetching data:

#.  First the method for computing the correlation and a data transformation setting
    have to be selected.

    Options are: *Pearson*, *Kendall*, or *Spearman*, and *raw*, *log2*, or *log10* respectively.

    |smartr_correlation_selection|

#.  The default view after creating the plot shows a scatter plot with the two selected nodes.
    Every dot represents an individual. On the axis bins are shown with counts for that
    specific range. A line is drawn that represents the calculated correlation and intersection.
    On the right some basic statistics are shown.

    |smartr_correlation_visualisation|

#.  Using the mouse, you can select a subgroup of individuals to recompute the basic statistics
    on the right. Also the correlation will be recomputed and redrawn. The selection box you've 
    created can be dragged. Right clicking it gives the option to zoom in on that area, to remove 
    those individuals from the computed statistics, or to reset the entire selection.

    |smartr_correlation_subselection|

.. note::

    You display values as coloured dots instead of black by including categorical values in the **Fetch data** step. 

Heatmap Workflow
~~~~~~~~~~~~~~~~

After fetching data the following control panel will be shown:

|smartr_heatmap_control| 

The panel provides the following options:

-   **Rows to show**: change this number to control the number of rows to show in the final heatmap. The 
    rows shown depends on the chosen *Ranking Criteria*.

-   **Group columns by**: you can set this to either *Node Order* or *Subject ID*. 

-   **GeneCard**: Set this to *Yes* to confirm you have read the terms of use for the GeneCards service.
    If this is left to *No*, then clicking on biomarkers in the corresponding heatmap rows will open the 
    relevant page at the EMBL EBI web service.

-   **Ranking criteria**: choose the metric to apply biomarker ranking. This will determine the order of
    rows in the heatmap. Options include metrics based on *Expression level*, *Expression variability*, and 
    *Differential expression*. The last option is only available when having defined two cohort subsets, 
    see `Heatmap: Differential expression`_.

The heatmap will appear after clicking **Create plot**.

|smartr_heatmap_hover|

By default the heatmap is sorted based on the chosen ranking criteria. The heatmap contains the following elements:

-   Rows for each of the selected (or all) biomarkers for the selected data node. Clicking on gene identifiers 
    takes you to external reference pages (GeneCards or EMBL EBI).
-   Columns for each individual in the chosen dataset.
-   Coloured squares based on the calculated z-score. The colour scheme can be changed in the `Heatmap: Toolbar`_.
    Hovering your mouse over the squares provides additional information.
-   Each row and column has a set of arrows that can be used to control the ordering of the heatmap. 

Below the heatmap itself you can find a table with detailed results.

|smartr_heatmap_table|


Heatmap: Toolbar
----------------

The toolbar in the bottom right of the window provides a set of functionalities to change the 
current representation of the heatmap.

|smartr_heatmap_toolbar|
 
-   **Marker statistic**: a dropdown that allows choosing several statistics that can be used 
    to display in the most left column of the heatmap. Available options: *coef*, *variance*, *range*, *mean*, and *median*.

-   **Colour scheme**: set the heatmap colours different multiple or single colour schemas.

-   **Zoom**: make everything smaller or bigger.

-   **Apply cutoff**: remove rows from the heatmap based on a cut-off on the chosen ranking criteria.

-   **Clustering**: the toolbar allows the user to create clustering instead of normal ordering, using
    the *R* functions for ``dist()`` for calculating distances and ``hclust()`` 
    (`docs <https://www.rdocumentation.org/packages/fastcluster/versions/1.1.24/topics/hclust>`__) for clustering.
    Computed are *Euclidean* and *Manhattan* distances with *complete*, *average*, and *single* clustering.

    Based on the chosen clustering the order of columns and rows will change to reflect the computed clusters.
    Dendrograms are shown to display the results.

    |smartr_heatmap_clustering|

Heatmap: Differential expression
--------------------------------

When having defined two cohort subsets some of the aspects of the analysis will be different. For one, the 
summary page that is shown after **Fetch data** will show information for both subsets. The heatmap control
panel will have the options for *Differential expression* enabled under **Ranking criteria**. This allows
the users to order the rows based on one off multiple differential expression metrics. 

The heatmap image itself will have an additional row to indicate to which subset an individual belongs. This bar 
allows researchers to easily identify the groups based after performing ordering or clustering.

|smartr_heatmap_differential_expression_image|

The table below the heatmap will show additional columns for: *TTEST*, *LOGFOLD*, *PVAL*, *ADJPVAL*, and *BVAL*. 
These measures that have been calculated between both subsets.

|smartr_heatmap_differential_expression_table|

Linegraph Workflow
~~~~~~~~~~~~~~~~~~

To create a graph, drag multiple *numerical* nodes from the same folder in the **Fetch data** step. The
graph shows the average and error for both subsets at every time point. Adding categorical nodes provides
boxed information per individual.

In the bottom of the screen a control bar is shown that contains:

-   Drop down to set the type of statistics to display: *mean* vs *median* and *SEM* vs *SD*
-   Tick boxes to *evenly space timepoints*, *Smooth graph*, and *User weighted events*

|smartr_linegraph|

.. important::
    For the line graph to model your data correctly, the nodes in the concept tree have to be arranged
    in a specific way. All nodes that belong to a single subfolder in the concept tree will be displayed
    in a single graph. If nodes originate from different subfolders, then multiple graphs will be shown.
    Like so:
    
    |smartr_linegraph_bad|

Volcanoplot Workflow
~~~~~~~~~~~~~~~~~~~~

The Volcanoplot allows you to use a high dimensional expression data set (not aCGH or VCF) 
to create the following plot:

|smartr_volcanoplot_main|


The blue (*logFC*) and red (*p-value*) lines are draggable and allow you to control the number of markers shown in the table on 
on the right. 

.. important::
    Because the Volcanoplot draws a very large number of elements on screen, not
    all web browsers will work seamlessly. Users might experience better performance
    with Google Chrome than Firefox for instance.


Undocumented workflows
----------------------

Currently the **Patientmapper** and **Ipaconnector** workflows are not documented here.


.. |smartr_main| image:: media/smartr_main.png
   :width: 8.0in
.. |smartr_empty_selection| image:: media/smartr_empty_selection.png
   :width: 8.0in
.. |smartr_selection_highdim| image:: media/smartr_selection_highdim.png
   :width: 8.0in
.. |smartr_fetch_summaries| image:: media/smartr_fetch_summaries.png
   :width: 5.0in
.. |smartr_boxplot| image:: media/smartr_boxplot.png
   :width: 8.0in
.. |smartr_correlation_selection| image:: media/smartr_correlation_selection.png
   :width: 3.0in
.. |smartr_correlation_visualisation| image:: media/smartr_correlation_visualisation.png
   :width: 8.0in
.. |smartr_correlation_subselection| image:: media/smartr_correlation_subselection.png
   :width: 8.0in
.. |smartr_heatmap_control| image:: media/smartr_heatmap_control.png
   :width: 5.0in
.. |smartr_heatmap_hover| image:: media/smartr_heatmap_hover.png
   :width: 8.0in
.. |smartr_heatmap_toolbar| image:: media/smartr_heatmap_toolbar.png
   :width: 6.0in
.. |smartr_heatmap_clustering| image:: media/smartr_heatmap_clustering.png
   :width: 8.0in
.. |smartr_heatmap_two_subsets_summaries| image:: media/smartr_heatmap_two_subsets_summaries.png
   :width: 8.0in
.. |smartr_heatmap_differential_expression_image| image:: media/smartr_heatmap_differential_expression.png
   :width: 8.0in
.. |smartr_heatmap_differential_expression_table| image:: media/smartr_heatmap_differential_expression_table.png
   :width: 8.0in
.. |smartr_heatmap_table| image:: media/smartr_heatmap_table.png
   :width: 8.0in
.. |smartr_linegraph| image:: media/smartr_linegraph.png
   :width: 8.0in
.. |smartr_linegraph_bad| image:: media/smartr_linegraph_bad.png
   :width: 4.0in
.. |smartr_volcanoplot_main| image:: media/smartr_volcanoplot_main.png
   :width: 8.0in
