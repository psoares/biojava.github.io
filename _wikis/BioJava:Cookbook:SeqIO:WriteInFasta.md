---
title: BioJava:Cookbook:SeqIO:WriteInFasta
---

How Do I Print A Sequence in Fasta Format?
------------------------------------------

FASTA format is a fairly standard bioinformatics output that is
convenient and easy to read. BioJava has a tools class called SeqIOTools
that provides static convenience methods to perform a number of common
bioinformatics IO tasks. The follwing snippets demonstrate how to print
a Sequence or even a whole SequenceDB in FASTA format to an OutputStream
like System.out. All of the WriteXX methods from SeqIOTools take an
OutputStream as an argument. In this way you can pipe the newly
formatted sequence to a file or another method or STDOUT, STDERR etc.

SeqIOTools is in the package org.biojava.bio.seq.io

### Printing a SequenceDB

          //make a instance of the SequenceDB interface
          SequenceDB db = new HashSequenceDB();

          //add the sequences to the DB
          db.addSequence(seq1);
          db.addSequence(seq2);

          /*
           * now print it to an output stream in FASTA format using a static method
           * from the utility class SeqIOTools. In this case our output stream is
           * STDOUT
           */
          SeqIOTools.writeFasta(System.out, db);

### Printing from a SequenceIterator

Many readXXX() methods from SeqIOTools return a SequenceIterator that
iterates over all the Sequences in a file. Most of teh writeXXX()
methods from SeqIOTools have a version of the methods that takes a
SequenceIterator as and argument eg.

          SequenceIterator iter =
              (SequenceIterator)SeqIOTools.fileToBiojava(fileType, br);

          //and now write it all to FASTA, (you can write to any OutputStream, not just System.out)
          SeqIOTools.writeFasta(System.out, iter);

### Printing a Single Sequence

          /*
           * SeqIOTools also has a method that takes a single sequence so you don't
           * have to make a SequenceDB
           */
          SeqIOTools.writeFasta(System.out, seq1);