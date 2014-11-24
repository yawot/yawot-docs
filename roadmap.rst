.. _libcellmlRoadmap:

=======
Roadmap
=======

David Nickerson, 9 June 2014

Contributions from Alan Garny, Jonathan Cooper, Mike Cooling, Tommy Yu, Hugh Sorby, Randall Britten and the CellML Community but no time yet for full consensus.

These requirements and milestones are derived from the `CellML API May 2014 Requirements <https://docs.google.com/document/d/1qMpltGGk19RgFAgkgnG8xZVKyI0Q-ZatcxV7VB_ccKc/edit>`_
collected from the CellML community, with input from the primary target users (application
developers) and the CellML Editorial Board. Previous editorial board discussions have also been
incorporated into this roadmap.

Clearly the milestones defined below are to be worked on in numerical order and previous milestones will be completed before work on subsequent milestones begins. Each milestone may consist of several 'releases' and future requirements may impact the design and implementation of earlier releases of libCellML. Major changes in the API will be accepted upto the release of libCellML version 1.0.0

.. contents::

High level objectives
=====================

#. Focus on CellML 1.2 and beyond.

  #. The implementation of libCellML should be driven by the requirements for supporting 1.2 and future versions.
  #. Implementing support for core+secondary specs is likely to be a big challenge for libCellML.

    #. libCellML should be designed to support the core spec with the flexibility for extra restrictions/constraints coming from the secondary specification.
    #. multiple secondary specifications could be used in one model.
    #. secondary specifications may exist for a period of time before they are integrated or consolidated into a new CellML version (if at all, there is still a lot to learn about how secondary specifications will evolve)

  #. libCellML should always be able to import earlier version models.
  #. To begin with, libCellML must be able to export 1.2 models to 1.1 (probably using API marked as deprecated from the beginning and removed once Milestone 3 is achieved).

#. Develop the libCellML API as work progresses through the milestones outlined below.

Environment
===========

This section will specify the environment for the development of libCellML.

* GitHub to host the primary libCellML source repository and issue tracker under the CellML organisation (editorial board members)
* Development language: C++ with SWIG bindings
* Build: CMake for generating cross-platform build rules
* Test: Using Buildbot on the BaTS to run continuous integration testing
* Test: Unit testing to use gtest
* Documentation: Written in re-Structured text.
* Documentation: API and source code examples will be documented using c++-style  doxygen comments.

Requirements
------------

* Documentation: Made available on readthedocs.org.  readthedocs uses Sphinx for generating documentation.
* Development: Agile and test driven development where:

  * Functionality more important than API stability in early releases.
  * Release early and often

* Development: Code review prior to acceptance into the primary repository using the pull request feature on GitHub
* Development: Objectives are added and broken down into incremental tasks
* Development: A single task should be no more than two weeks
* Development: The next objective to be worked on is discussed and agreed with the community before work is started on an objective

We should avoid using non-standard system libraries unless there is a compelling reason.  Once features are available the API can be fine tuned in consultation with the CellML community.

Milestone 0: setting up development environment (timeframe: 8 working days)
===========================================================================

**To be completed on Wednesday 3rd September 2014**

#. Share an UML-esque document with the community via github describing CellML specific object model.

   * The form of the API to libCellML should not be dictated by the XML serialisation but by the objects tool developers desire to work with.

#. Setup the cross platform build and test environment using the ABI's build and test server (BaTS)

   * Builds required: Windows 64 bit, OSX 10.9, Ubuntu 14.04 64 bit

#. Document the development process/workflow

   * How we are to implement agile and test driven development
   * How code reviews are done

Milestone 1: starting to get useful code (timeframe: ? months)
==============================================================

#. Create a CellML 1.2 model from scratch and save it to XML
   
   #. create a new model, add imports, components, variables, and math.
   #. the first test case?
   
#. Load a CellML 1.2 model, make changes, save it.
   
   #. ability to preserve underlying XML structure/ordering for documents read in and written out.

#. Load a CellML 1.2 model and validate it
   
   #. this is important to get out early as it will help make sure the normative specification is *complete* and sensible.
   #. will ensure we can test models as we work on getting the specification completed (c.f. the error ridden examples from 1.0 and 1.1 specifications).
   #. includes proper units validation of the mathematics.
   #. libCellML should have a validation framework based on the core specification and then secondary specs can add their specific rules

#. for 1.2 this is mainly the mathematics, so core validation can probably validate the model but need the actual restricted subset of mathml from the secondary spec is needed to fully validate units consistency.
#. Import CellML 1.0/1.1 models.
#. Export to CellML 1.1 in order to use model in existing tools (e.g., simulation, annotation, NeSI), preserving model and XML structure/ordering/modularity where possible.
#. Platform support: OS X, Linux, Windows
   
   #. native installers (using CPack, pip)
   #. easy to setup build environment (good documentation)

#. Language support: C++, Python, Java, Matlab
#. Documentation available
   
   #. API
   #. Tutorials/documented code examples
   #. Integrating libCellML into various common IDEs (Visual Studio, Eclipse, Qt Creator, NetBeans*)
   
Milestone 2: toward simulation support (timeframe: ? months)
============================================================

#. Conversion to intermediate representation
   
   #. Conversion to CellMLstructureless mathematics (just the maths) into an intermediate representation that can be transformed / analysed by other tools. With units.
   #. Ability to maintain the CellML structure (as much as possible), perhaps via object annotation (e.g., COR)
   #. Will form the basis for tools using libCellML to perform numerical simulation.
   
#. Improved support for model authoring/editing/manipulation
   
   #. Provide an events system to monitor changes in the model
   #. provide access to data contained in CellML models in external namespaces (RDF, extensions, etc).

#. Documentation, documentation, documentation.

Milestone 3: functional library for tool developers (timeframe: ? months)
=========================================================================

#. Establish the process/API required to generate procedural code from the intermediate representation

   #. Generic code vs solver specific code.
   #. Could be a role for being informed from SED-ML what solver is to be used and customising generated code appropriately.
   #. Would be a tool sitting on top of libCellML, not directly part of it.

#. Being able to run simulations with CellML 1.2

   #. while not directly part of libCellML, helping tool developers get to the point where they can execute simulations is critically important.
   #. CellML 1.2 will not be released until we can do this (in addition to the other requirements above)

Milestone 4: advanced capabilities (timeframe: ? months)
========================================================

#. High order model manipulation (recall discussion with Andrew McCulloch at the 8th workshop)
   
   #. again, outside core libCellML, but helping tool developers provide these kinds of services is very important.

Milestone 5: broadening accessibility (timeframe: ? months)
===========================================================

#. Support for more platforms

   #. Android, iOS

#. and languages
   
   #. JS, C#/.NET, C, Fortran[77|90|20XX]

