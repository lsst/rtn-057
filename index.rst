:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**

Abstract
========

Description of the L3 milestone for early DRP type processing.

Introduction
============

This document serves as a description of the milestone USDF ready for ComCam processing as
well as a report on testing to achieve the milestone. The operations milestone ticket for this
is PREOPS-1667. The description is in Section 3 while the test status is in Section 4.

Milestone Description
=====================

Annual Data Release Processing is planned to be a multi-site activity with the facilities in France, the UK and the US, wherein all data taken to date are reprocessed withe the latest algorithms and calibrations.  It is anticipated that the Rucio and FTS tools will be used for data distribution and PanDA for distributed workflow. All three servers should be in production at the USDF.  A key goal of this work is to demonstrate processing at a sufficient rate


Based on `DMTN-213 <https://dmtn-213.lsst.io/>`__, here is a description of multi-site DRP processing.  We assume that a local source Butler and registry have been set up at each Data Facility (DF) with a skymap and reference catalogs, but not necessarily with calibration products.  We also assume that each DF will handle processing for a contiguous subset of skymap patches that are unique to that DF.

#. Calibration products are replicated to each DF and ingested into the local source Butler by the Replica Monitor.
#. Campaign Management tooling (CMt) determines which raw visit data should be copied to each DF to support coadd generation (step 3) and later processing and to minimize downstream data movement.  We assume individual visits will not be subdivided between DFs, i.e., DFs will only consider whole visits.
#. CMt generates the yaml files, for all steps (1-9), specific to each DF.
#. Raw data are replicated as necessary to Fr and UK DFs, and the Replica Monitor ingests raw data into the local source Butler at each DF.
#. For each step in (1..9):

  #. BPS generates QuantumGraphs (QGs) and Execution Butlers (EBs) from the yamls at USDF.
  #. Needed data for the current step are replicated from USDF to the remote DF.
  #. PanDA/BPS submits the workflows from USDF to the corresponding DFs.
  #. When the workflows finish, they merge the EB into the local source Butler. The relevant datasets are also registered with Rucio.
  #. Rucio replicates appropriate subsets of the remote data back to USDF, where they are ingested into the USDF Butler.

Notes:

- Aside from the final, non-temporary data products that will be replicated to USDF, the only other data that needs to be transferred will be the PVIs that are needed for coadd generation at a given DF.  These PVIs will be in the "overlap regions" of their corresponding visit and the sky patches that are assigned to the neighboring regions assigned to the other DFs.  Since PVIs are "final" data products, they will all be copied to USDF and can be transferred to remote DFs from USDF as needed.
- It's unclear how temporaries like the warps will be handled.  They need to be in the Butler registry in order for the QGs to be generated.  If all QGs are generated at USDF, then data like the warps needed to be in the USDF registry, but presumably not copied to USDF.  Are they registered with Rucio URIs?  Do we have that capability?
- The above sequence assumes we will be using the DC2 test-med-1 dataset, which does not include global calibration at the tail end of single frame processing.  The global calibration steps are part of HSC processing (see steps 2b-e in the `HSC DRP-Prod pipelne <https://github.com/lsst/drp_pipe/blob/main/pipelines/HSC/DRP-Prod.yaml#L43>`__), and (I think) they require all of the visit-level catalog data to be processed at a single site, i.e., at USDF, before proceeding with steps 3 and later.  Should we consider an HSC data set instead for these tests?

Tests and Test Status
=====================

Distribution of raw input data to all sites
-------------------------------------------

Distribution of processing graphs
---------------------------------

Registration of output products
-------------------------------

Distribution of output products
-------------------------------
 
Demonstrate processing at a sufficient rate
-------------------------------------------

See the `reStructuredText Style Guide <https://developer.lsst.io/restructuredtext/style.html>`__ to learn how to create sections, links, images, tables, equations, and more.

.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
