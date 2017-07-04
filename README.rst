Welcome to transmartApp documention home.

Making changes to the manual
----------------------------

General process
---------------
* in your own branch change the text
* commit changes to your own branch and push to own branch
Eventually commit and push to master


Documentation
-------------
* View manual document: (format) `<http://transmart-app.readthedocs.io/>`_
* Status of page/document building process: `<https://readthedocs.org/projects/transmart-app/builds/>`_
* Information on restructured text as used by Sphinx. Read this before contributing: `http://www.sphinx-doc.org/en/stable/rest.html`_


General textual changes made
----------------------------
changes in documents in folder "source".

* removed all references to actual page numbers in the manual
* added links where missing
* removed , before the word "and" 
* added quotation marks for concepts used in TM (at least when first mentioned in the text)

Creating links:
------------
Within a document: 

* `link text <header-name>`__(e.g. `Active Filters <#managing-active-filters>`__)
* or, directly referencing a title (e.g. `Running the Analyses`_,)

to another document in the project folder: 

* create a link anchor above the header you want to link to: .. _running-the-analysis-label:
* then create a link to it using :ref:`running-the-analysis-label`
