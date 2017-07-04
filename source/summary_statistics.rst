Chapter 4: Summary Statistics
=============================

This chapter explains how to review study information and populate the
cohorts you use for analyses.

.. _generating-summary-statistics-label:

Generating Summary Statistics
-----------------------------

When you finish defining criteria for the cohorts to compare — the
subsets — click the **Summary Statistics** button.

.. note::
    As an alternative to generating summary statistics, you can view a breakdown 
    of a particular subset by a selected concept (see `View Subset Breakdown by Concept`_).   

tranSMART displays tables and charts of information that describe the
subsets. The information is displayed in Summary Statistics view in the
following sections:

    A summary of the criteria used to define subsets to compare.

    For example:

    |image76|

    A table showing the number of subjects in each subset that match the subset criteria.

    For example:

    |image77|

    In this example, 58 subjects matched the criteria for Subset 1 and
    63 matched the criteria for Subset 2. No (0) subjects matched the
    criteria for both subsets.
   
    Tables and charts that show how the subjects who match the criteria
    fit into age, sex, and race demographics.

    This example shows the age portion of the demographics data only:

    |image78|

    Analyses of the concepts you added to the subsets from the navigation
    tree. The data displayed reflects the data used to generate the
    summary statistics.

The next examples show analysis of concepts for a non-linked event, a
linked event, and NGS data.

    |image79|

    **Example 1: Non-linked event.** 
    
    This example shows the analysis of the chemotherapy concept:

    |image80|

    **Example 2: Linked event.** 
    
    This example shows the analysis of concepts for adverse events:

    |image81|

    **Example 3: NGS data.** 
    
    This example shows the analysis of concepts for description of planned arm:

Significance Tests
~~~~~~~~~~~~~~~~~~

The analyses include the results of significance testing that Analyze
performs:

|image82|

Significance testing is designed to indicate whether the reliability of
the statistics is 95% or greater, based on p-value.

Analyze calculates the significance result using either t-test or
chi-squared statistics to determine the p-value:

-   For continuous variables (for example, subject weight or age), a
    t-test compares the observed values in the two subsets.
    
    See `this <http://commons.apache.org/math/apidocs/org/apache/commons/math4/stat/inference/TTest.html#tTest(double[],%20double[])>`__ 
    if you're interested in the Java method used to calculate the t-test statistic.

-   For categorical values (for example, diagnoses), a chi-squared test
    compares the counts in the two subsets.

    See `this <http://commons.apache.org/math/apidocs/org/apache/commons/math4/stat/inference/ChiSquareTest.html#chiSquareTest(long[][])>`__ 
    for the Java method that calculates the chi-squared statistic.


If there is not enough data to calculate a test, Analyze displays a
message indicating the insufficient quantity of data. In addition,
significance test results are not displayed in the following
circumstances:

-   If two identical subsets are defined. In this case, the significance
    test results are not meaningful.

-   If all subjects in the first subset have one set of values for the
    categorical value and all subjects in the second subset have other
    categorical values. For example, suppose you set Subset 1 to contain
    only males and Subset 2 to contain only females. If you then try to
    show statistics by gender, tables similar to the following would
    result:

    |image83|

    In this case, the chi-squared function doesn’t return meaningful
    results.


View Subset Breakdown by Concept
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generating summary statistics provides data for all subsets defined by
study cohorts. You can view data for a particular subset, however, as
follows:

#.  Select a cohort from the navigation tree and drag it into a subset; for example:

    |image84|

#.  Click the **Summary Statistics** tab.

#.  Drag and drop a folder from the navigation tree into the empty page;
    for example:

    |image85|

#.  tranSMART calculates the results and displays the data for the given subset and concept:

    |image86|


Defining Points of Comparison
-----------------------------

Once you establish the subsets of subjects that you want to compare, you
can apply one or more points of comparison to the subsets. A *point of
comparison* is a concept in the navigation tree.

To apply a point of comparison to the subsets:

#.  You must already have defined the subsets and have generated summary 
    statistics for the subsets, as described in the previous section.

#.  Drag the concept that you want to introduce as the point of
    comparison from the navigation tree and drop it anywhere inside
    the Summary Statistics view.

As soon as you drop the point of comparison into the Summary Statistics
view, tranSMART begins to compare the subsets based on that point of
comparison. When finished, tranSMART displays a side-by-side summary of
how the subjects in each subset match or respond to the point of
comparison.

Results of a Comparison
~~~~~~~~~~~~~~~~~~~~~~~

In a comparison of subjects in a psychological study, suppose Subset 1
contains subjects with a substance abuse problem and Subset 2 contains
subjects with no substance abuse assessment.

After the subsets are defined and summary statistics are generated, a
diagnosis of depression is dropped into the Summary Statistics view as a
point of comparison. tranSMART displays a side-by-side comparison of the
subjects in each subset, indicating that almost all the subjects with a
substance abuse problem have been diagnosed with depression, while that
diagnosis for those with no substance abuse problem is more evenly
split.

The comparison is placed at the top of the Summary Statistics view,
above the demographic definitions plus any other earlier comparisons:

|image87|

.. note::
    To keep the size of the preceding figure within production limits, 
    the demographics (age, sex, and race) portions of the figure are excluded.

.. note::
    Query details accessed through the **Summary** button do not reflect points of comparison.

    
Printing the Contents of Summary Statistics View
------------------------------------------------

You can print the contents of Summary Statistics view as shown below.

#.  In Summary Statistics view, click the **Print** button:

    |image90|

    The entire contents of Summary Statistics view appear in a separate browser window.

#.  Click **Print this page**.


Copying Individual Charts in Summary Statistics View
----------------------------------------------------

If you are interested in a particular chart in the Summary Statistics
view, you can copy the chart to a file, as follows:

#.  With the Summary Statistics view displayed, click **Print**.

    The entire contents of the Summary Statistics view appear in a separate
    browser window.

#.  Right-click the chart you want to copy.

#.  In the Internet Explorer popup menu, click **Save Image As**.

#.  In the Save Image dialog, specify the name, location, and the file
    type for the chart.

#.  Click **Save**.


.. _viewing-analysis-data-in-grid-view-label:

Viewing Analysis Data in Grid View
----------------------------------

If you are displaying analysis data in the various tables and charts of
Summary Statistics view, and want to view the data in a single table,
use the **Grid View** option.

Access Grid View as follows:

#.  Click the **Analyze** tool and define your cohorts as described earlier in this chapter.

#.  Click **Summary Statistics**.

#.  Click **Grid View**.

    |image91|

#.  Optionally, you can drag and drop additional points of comparison
    into the grid, and new columns will appear for that data.

#.  You can drag a node from any level of the tree into the grid.

Sample of Grid View for a public study:

|image92|

.. note::
	 The ID assigned in the **Subject** column is the internal tranSMART ID that is assigned at the time of data loading. The ID in the **Patient** field contains the original subject ID that was provided in the data.   

Grid View Display Options
~~~~~~~~~~~~~~~~~~~~~~~~~

-   **Sort the grid by a specific column.** Click the down-arrow icon
    (|image94|) next to the column heading you want to sort by, then
    select **Sort Ascending** or **Sort Descending**.

-   **Hide or redisplay columns.** Click the down-arrow icon next to any
    column heading, click **Columns** as shown below, then select or
    deselect columns to hide or redisplay:

    |image95|

If a column name does not appear in the menu, you have not included the
associated concept in the analysis. For example, Diagnosis has not been
included in the analysis above.

.. |image76| image:: media/image63.png
   :width: 6.00000in
   :height: 0.80486in
.. |image77| image:: media/image64.png
   :width: 1.68729in
   :height: 0.73949in
.. |image78| image:: media/image65.png
   :width: 6.00000in
   :height: 2.29444in
.. |image79| image:: media/image66.png
   :width: 6.00000in
   :height: 2.35347in
.. |image80| image:: media/image67.png
   :width: 6.00000in
   :height: 5.18819in
.. |image81| image:: media/image68.png
   :width: 5.87106in
   :height: 4.45833in
.. |image82| image:: media/image69.png
   :width: 3.01004in
   :height: 0.77074in
.. |image83| image:: media/image70.png
   :width: 6.00000in
   :height: 1.38264in
.. |image84| image:: media/image71.png
   :width: 6.00000in
   :height: 1.42500in
.. |image85| image:: media/image72.png
   :width: 6.00000in
   :height: 2.34792in
.. |image86| image:: media/image73.png
   :width: 6.00000in
   :height: 4.50764in
.. |image87| image:: media/image74.png
   :width: 6.37851in
   :height: 2.04167in
.. |image90| image:: media/image75.png
   :width: 6.00000in
   :height: 1.42917in
.. |image91| image:: media/image76.png
   :width: 3.98908in
   :height: 0.57285in
.. |image92| image:: media/image77.png
   :width: 6.00000in
   :height: 1.93542in
.. |image94| image:: media/image78.png
   :width: 0.10417in
   :height: 0.17361in
.. |image95| image:: media/image79.png
   :width: 3.17669in
   :height: 3.46832in