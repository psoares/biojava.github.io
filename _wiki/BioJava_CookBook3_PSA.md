---
title: BioJava:CookBook3:PSA
permalink: wiki/BioJava%3ACookBook3%3APSA
---

How to create a Pairwise Sequence Alignment in BioJava
======================================================

Global alignment
----------------

```java

package org.biojava.nbio.alignment;

import java.net.URL;

import org.biojava.nbio.alignment.Alignments.PairwiseSequenceAlignerType;
import org.biojava.nbio.alignment.template.SequencePair;
import org.biojava.nbio.alignment.template.SubstitutionMatrix;
import org.biojava.nbio.core.sequence.ProteinSequence;
import org.biojava.nbio.core.sequence.compound.AminoAcidCompound;
import org.biojava.nbio.core.sequence.io.FastaReaderHelper;

public class CookbookAlignPairGlobal {

   public static void main(String[] args) {
       String[] ids = new String[] {"Q21691", "Q21495", "O48771"};
       try {
           alignPairGlobal(ids[0], ids[1]);
       } catch (Exception e){
           e.printStackTrace();
       }
   }

   private static void alignPairGlobal(String id1, String id2) throws Exception {
       ProteinSequence s1 = getSequenceForId(id1), s2 = getSequenceForId(id2);
       SubstitutionMatrix<AminoAcidCompound> matrix = new SimpleSubstitutionMatrix<AminoAcidCompound>();
       SequencePair<ProteinSequence, AminoAcidCompound> pair = Alignments.getPairwiseAlignment(s1, s2,
               PairwiseSequenceAlignerType.GLOBAL, new SimpleGapPenalty(), matrix);
       System.out.printf("%n%s vs %s%n%s", pair.getQuery().getAccession(), pair.getTarget().getAccession(), pair);
   }

   private static ProteinSequence getSequenceForId(String uniProtId) throws Exception {
       URL uniprotFasta = new URL(String.format("[http://www.uniprot.org/uniprot/%s.fasta](http://www.uniprot.org/uniprot/%s.fasta)", uniProtId));
       ProteinSequence seq = FastaReaderHelper.readFastaProteinSequence(uniprotFasta.openStream()).get(uniProtId);
       System.out.printf("id : %s %s%n%s%n", uniProtId, seq, seq.getOriginalHeader());
       return seq;
   }

}

```

Local alignment
---------------

```java

package org.biojava.nbio.alignment;

import java.net.URL;

import org.biojava.nbio.alignment.Alignments.PairwiseSequenceAlignerType;
import org.biojava.nbio.alignment.template.SequencePair;
import org.biojava.nbio.alignment.template.SubstitutionMatrix;
import org.biojava.nbio.core.sequence.ProteinSequence;
import org.biojava.nbio.core.sequence.compound.AminoAcidCompound;
import org.biojava.nbio.core.sequence.io.FastaReaderHelper;

public class CookbookAlignPairLocal {

   public static void main(String[] args) {
       String[] ids = new String[] {"Q21691", "Q21495", "O48771"};
       try {
           alignPairLocal(ids[0], ids[1]);
       } catch (Exception e){
           e.printStackTrace();
       }
   }

   private static void alignPairLocal(String id1, String id2) throws Exception {
       ProteinSequence s1 = getSequenceForId(id1), s2 = getSequenceForId(id2);
       SubstitutionMatrix<AminoAcidCompound> matrix = new SimpleSubstitutionMatrix<AminoAcidCompound>();
       SequencePair<ProteinSequence, AminoAcidCompound> pair = Alignments.getPairwiseAlignment(s1, s2,
               PairwiseSequenceAlignerType.LOCAL, new SimpleGapPenalty(), matrix);
       System.out.printf("%n%s vs %s%n%s", pair.getQuery().getAccession(), pair.getTarget().getAccession(), pair);
   }

   private static ProteinSequence getSequenceForId(String uniProtId) throws Exception {
       URL uniprotFasta = new URL(String.format("http://www.uniprot.org/uniprot/%s.fasta", uniProtId));
       ProteinSequence seq = FastaReaderHelper.readFastaProteinSequence(uniprotFasta.openStream()).get(uniProtId);
       System.out.printf("id : %s %s%n%s%n", uniProtId, seq, seq.getOriginalHeader());
       return seq;
   }

}

```

How to concurrently create a PSA for each pair in a sequence list in BioJava
============================================================================

Global alignments
-----------------

```java

package org.biojava3.alignment;

import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import org.biojava.nbio.alignment.Alignments.PairwiseSequenceAlignerType;
import org.biojava.nbio.alignment.template.SequencePair;
import org.biojava.nbio.alignment.template.SubstitutionMatrix;
import org.biojava.nbio.core.sequence.ProteinSequence;
import org.biojava.nbio.core.sequence.compound.AminoAcidCompound;
import org.biojava.nbio.core.sequence.io.FastaReaderHelper;
import org.biojava.nbio.core.util.ConcurrencyTools;

public class CookbookAlignAllGlobal {

   public static void main(String[] args) {
       String[] ids = new String[] {"Q21691", "Q21495", "O48771"};
       try {
           alignAllGlobal(ids);
       } catch (Exception e){
           e.printStackTrace();
       }
   }

   private static void alignAllGlobal(String[] ids) throws Exception {
       List<ProteinSequence> lst = new ArrayList<ProteinSequence>();
       for (String id : ids) {
           lst.add(getSequenceForId(id));
       }
       SubstitutionMatrix<AminoAcidCompound> matrix = new SimpleSubstitutionMatrix<AminoAcidCompound>();
       List<SequencePair<ProteinSequence, AminoAcidCompound>> alig = Alignments.getAllPairsAlignments(lst,
               PairwiseSequenceAlignerType.GLOBAL, new SimpleGapPenalty(), matrix);
       for (SequencePair<ProteinSequence, AminoAcidCompound> pair : alig) {
           System.out.printf("%n%s vs %s%n%s", pair.getQuery().getAccession(), pair.getTarget().getAccession(), pair);
       }
       ConcurrencyTools.shutdown();
   }

   private static ProteinSequence getSequenceForId(String uniProtId) throws Exception {
       URL uniprotFasta = new URL(String.format("http://www.uniprot.org/uniprot/%s.fasta", uniProtId));
       ProteinSequence seq = FastaReaderHelper.readFastaProteinSequence(uniprotFasta.openStream()).get(uniProtId);
       System.out.printf("id : %s %s%n%s%n", uniProtId, seq, seq.getOriginalHeader());
       return seq;
   }

}

```

Local alignments
----------------

```java

package org.biojava3.alignment;

import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import org.biojava.nbio.alignment.Alignments.PairwiseSequenceAlignerType;
import org.biojava.nbio.alignment.template.SequencePair;
import org.biojava.nbio.alignment.template.SubstitutionMatrix;
import org.biojava.nbio.core.sequence.ProteinSequence;
import org.biojava.nbio.core.sequence.compound.AminoAcidCompound;
import org.biojava.nbio.core.sequence.io.FastaReaderHelper;
import org.biojava.nbio.core.util.ConcurrencyTools;

public class CookbookAlignAllLocal {

   public static void main(String[] args) {
       String[] ids = new String[] {"Q21691", "Q21495", "O48771"};
       try {
           alignAllLocal(ids);
       } catch (Exception e){
           e.printStackTrace();
       }
   }

   private static void alignAllLocal(String[] ids) throws Exception {
       List<ProteinSequence> lst = new ArrayList<ProteinSequence>();
       for (String id : ids) {
           lst.add(getSequenceForId(id));
       }
       SubstitutionMatrix<AminoAcidCompound> matrix = new SimpleSubstitutionMatrix<AminoAcidCompound>();
       List<SequencePair<ProteinSequence, AminoAcidCompound>> alig = Alignments.getAllPairsAlignments(lst,
               PairwiseSequenceAlignerType.LOCAL, new SimpleGapPenalty(), matrix);
       for (SequencePair<ProteinSequence, AminoAcidCompound> pair : alig) {
           System.out.printf("%n%s vs %s%n%s", pair.getQuery().getAccession(), pair.getTarget().getAccession(), pair);
       }
       ConcurrencyTools.shutdown();
   }

   private static ProteinSequence getSequenceForId(String uniProtId) throws Exception {
       URL uniprotFasta = new URL(String.format("http://www.uniprot.org/uniprot/%s.fasta", uniProtId));
       ProteinSequence seq = FastaReaderHelper.readFastaProteinSequence(uniprotFasta.openStream()).get(uniProtId);
       System.out.printf("id : %s %s%n%s%n", uniProtId, seq, seq.getOriginalHeader());
       return seq;
   }

}

```
