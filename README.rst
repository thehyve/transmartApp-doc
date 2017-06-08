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
* View manual document: (format) `<http://transmart-app.readthedocs.io/en/jolandas-patch-1/>`_
* Status of page/document building process: `<https://readthedocs.org/projects/transmart-app/builds/>`_
* Information on restructured text (used in Github to indicated formatating of text) `<http://openalea.gforge.inria.fr/doc/openalea/doc/_build/html/source/sphinx/rest_syntax.html#headings>`_


General textual changes made
----------------------------
changes in documents in folder "source".
* removed all references to actual page numbers in the manual
* added links where missing
* removed , before the word "and" 
* added quotation marks for concepts used in TM (at least when first mentioned in the text)

Setup links:
------------
within a document: `link text <header-name>`__(e.g. `Active Filters <#managing-active-filters>`__)
to another document in the project folder: `link text <file.rst#header>'_ (e.g. `here <admin.rst#browse-tool-administration>`_, between brackets is the last part of the specific URL which you can find when clicking on the link sign next to a header in a document)
