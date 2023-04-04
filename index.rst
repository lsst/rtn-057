:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**

Abstract
========

Description of the L2 milestone for early DRP type processing.

Introduction
============

This document serves as a description of the milestone USDF ready for ComCam processing as
well as a report on testing to achieve the milestone. The operations milestone ticket for this
is PREOPS-1667. The description is in Section 3 while the test status is in Section 4.

Milestone Description
=====================

Annual Data Release Processing is planned to be a multi-site activity with the facilities in France, the UK and the US, wherein all data taken to date are reprocessed withe the latest algorithms and calibrations.

The elements of a DRP are:
 - distribution of raw input data to all sites
 - distribution of processing graphs
 - registration of output products (in the butler and Rucio)
 - distribution of output products back to the USDF for the central archive and to the other Data Facilities as needed.
 - demonstrate processing at a sufficient rate
 
 It is anticipated that the Rucio and FTS tools will be used for data distribution and PanDA for distributed workflow. All three servers should be in production at the USDF.

Tests and Test Status
=====================

distribution of raw input data to all sites
-------------------------------------------

distribution of processing graphs
---------------------------------

registration of output products
-------------------------------

distribution of output products
-------------------------------
 
demonstrate processing at a sufficient rate
-------------------------------------------

See the `reStructuredText Style Guide <https://developer.lsst.io/restructuredtext/style.html>`__ to learn how to create sections, links, images, tables, equations, and more.

.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
