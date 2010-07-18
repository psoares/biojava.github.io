---
title: BioJava3 NCBISequenceReader Design
---

Introduction
------------

The ***NCBISequenceReader*** class, part of the biojava-core project,
retrieves data from the [NCBI](http://www.ncbi.nlm.nih.gov/) website
using the [eutils](http://eutils.ncbi.nlm.nih.gov/) via a HTTP GET
request. The SOAP interface was not pursued due to advice from other
contributors to this project.

Design Overview
---------------

Coming soon...

Design Issues
-------------

The following issues have come up during the implementation and need to
be resolved.

### Exceptions

The class inherits the methods **getSequence()** and
**getSequenceAsString(Integer start, Integer end, Strand strand)** from
the ***AbstractSequence*** since these methods need to establish a
connection to the NCBI website there are going to be times when the
connection will fail, an invalid nucleotide identifier is passed in to
the constructor or any other host of issues.

Ideally, the methods should throw a ***SequenceException*** which will
be a generic exception, wrapping any exceptions generated by the
implementing classes.

### Logging

using log4j would be very useful!

Testing
-------

The table below shows a summary of the unit tests created for the
NCBISequenceReader class.

| Test Name (method) | Description | Seed data | Requires network (Y/N) |
|--------------------|-------------|-----------|------------------------|
| Cell 1             | Cell 2      | Cell 3    | Cell 4                 |
| Cell A             | Cell B      | Cell C    |

