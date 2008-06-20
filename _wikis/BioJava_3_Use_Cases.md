---
title: BioJava 3 Use Cases
---

This page will contain a bunch of use-cases which will drive development
for BioJava 3. Please add them below - as simple or as complex as you
wish!

Use cases
---------

-   Multiple GenBank sequences inside a single file
    (ftp://bio-mirror.net/biomirror/genbank/gbbct1.seq.gz) can be easily
    indexed.
-   Is it possible to write the sequence to any object instead of
    writing it to a PrintStream?

`           // existing method`  
`           genbankFormat.writeSequence(richSequence, printStream);`