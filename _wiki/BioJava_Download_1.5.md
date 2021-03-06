---
title: BioJava:Download 1.5
permalink: wiki/BioJava%3ADownload_1.5/
---

This page offers downloads for the BioJava 1.5 release. BioJava 1.5 runs
on Java 2 Standard Edition 1.4.2 (or later) platforms.

A release candidate for the next verision of BioJava (1.6) is available
from <BioJava:Download_1.6>. This is the first BioJava release running
with Java 1.5 (or later).

Complete Download
-----------------

A complete download is available as one
[tar](http://www.biojava.org/download/bj15/all/BioJava1.5-all.tar) file
(16Mb). The file contains all binaries, required jars, docs, source,
test, demos and apps as gzipped tar files.

BioJava binaries
----------------

A complete binary distribution is available as one large
[gzip](http://www.biojava.org/download/bj15/bin/BioJava1.5-bin.tar.gz)
file (3.5Mb). It contains the biojava.jar as well as the apps.jar,
demos.jar and the supporting libraries.

The apps.jar contains some simple example apps built with biojava. The
demos.jar contains some simple demo programs (some are a bit dated).
Refer to the [cookbook](/wiki/BioJava:Cookbook "wikilink") for more up to date
examples.

### Support libraries

-   bytecode.jar: Required to run biojava
-   commons-cli.jar: Only required to compile and use some of the demos
-   commons-collections-2.1.jar: only required for some demos and BioSQL
    access (and building biojava.jar)
-   commons-dbcp-1.1.jar: Only required for legacy BioSQL access (and
    building biojava.jar)
-   commons-pool-1.1.jar: Only required for legacy BioSQL access (and
    building biojava.jar)

Source Files
------------

The full source distribution is available as a
[gzip](http://www.biojava.org/download/bj15/src/BioJava1.5-src.tar.gz)
file (7.8Mb) that can be built using ant.

Documentation
-------------

Documentation is available as a
[gzip](http://www.biojava.org/download/bj15/doc/BioJava1.5-docs.tar.gz)
file (4.5Mb) that includes the javadocs for the API, demos and apps.

Latest builds
-------------

To get the very latest version of BioJava that is automatically built
from the latest CVS version, please go
[here](http://www.spice-3d.org/cruise/). Also available is the nightly
[BioJava
javadoc](http://www.spice-3d.org/public-files/javadoc/biojava/index.html)

CVS access
----------

the CVS repository can be browsed at:
<http://code.open-bio.org/cgi/viewcvs.cgi/biojava-live/?cvsroot=biojava>

An RSS of biojava-live is
[available](http://www.biojava.org/CVS2RSS/biojava-live.rss)

To obtain an anonymous CVS checkout do the following:

`  cvs -d :pserver:cvs@code.open-bio.org:/home/repository/biojava login`

-   When prompted, the password is 'cvs'
-   Each project CVS repository can have many different packages
    available for download. You may need to browse the web interface for
    a bit to determine the packages of interest. After a successful
    login you may "checkout" the project package you are interested in.

The following command should be executed as one line.

`  cvs -d :pserver:cvs@code.open-bio.org:/home/repository/biojava checkout biojava-live`

-   The login and checkout procedure should only have to be done once.
    To update the source directories in the future it should be possible
    just to enter the top level directory and issue the following
    command:

`  cvs update -dP`

Getting older versions
----------------------

-   The legacy release of 1.4 can be found
    [here](/wiki/BioJava:Download 1.4 "wikilink")
-   The legacy release 1.3 can be found
    [here](/wiki/BioJava:Download 1.3 "wikilink").
-   Older releases of BioJava can be found in the [download
    area](http://www.biojava.org/download/).

