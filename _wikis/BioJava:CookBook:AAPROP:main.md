---
title: BioJava:CookBook:AAPROP:main
---

### How can I compute physico-chemical properties?

BioJava provides a set of APIs to generate some commonly used
physiochemical properties. They are

-   [Molecular
    Weight](http://biojava.org/wiki/BioJava:CookBook:AAPROP:molecularweight)
-   [Absorbance](http://biojava.org/wiki/BioJava:CookBook:AAPROP:absorbanceandextinctioncoefficient)
-   [Extinction
    Coefficient](http://biojava.org/wiki/BioJava:CookBook:AAPROP:absorbanceandextinctioncoefficient)
-   [Instability
    Index](http://biojava.org/wiki/BioJava:CookBook:AAPROP:instabilityindex)
-   [Apliphatic
    Index](http://biojava.org/wiki/BioJava:CookBook:AAPROP:apliphaticindex)
-   [Average Hydropathy
    Value](http://biojava.org/wiki/BioJava:CookBook:AAPROP:averagehydropathyvalue)
-   [Isoelectric
    Point](http://biojava.org/wiki/BioJava:CookBook:AAPROP:isoelectricpoint)
-   [Net Charge at pH
    7](http://biojava.org/wiki/BioJava:CookBook:AAPROP:netcharge)
-   Composition of specified amino acid
-   Composition of the 20 standard amino acid

The class providing the core functionality for this is the
IPeptideProperties class.

Short Example 1: Computing molecular weight using default values
----------------------------------------------------------------

<java> String sequence =
"QIKDLLVSSSTDLDTTLVLVNAIYFKGMWKTAFNAEDTREMPFHVTKQESKPVQMMCMNNSFNVATLPAE";
System.out.println("Molecular Weight: " +
PeptideProperties.getMolecularWeight(sequence)); </java>

Short Example 2: Computing molecular weight using user-defined values
---------------------------------------------------------------------

<java> String sequence =
"QIKDLLVSSSTDLDTTLVLVNAIYFKGMWKTAFNAEDTREMPFHVTKQESKPVQMMCMNNSFNVATLPAE";
File elementMassFile = new File("./src/main/resources/ElementMass.xml");
File aminoAcidCompositionFile = new
File("./src/main/resources/AminoAcidComposition.xml");
System.out.println("Molecular Weight: " +
PeptideProperties.getMolecularWeight(sequence, elementMassFile,
aminoAcidCompositionFile)); </java>

Short Example 3: Computing molecular weight for multiple sequences
------------------------------------------------------------------

<java> String[] sequences = new String[3]; sequences[0] =
"QIKDLLVSSSTDLDTTLVLVNAIYFKGMWKTAFNAEDTREMPFHVTKQESKPVQMMCMNNSFNVATLPAE";
sequences[1] =
"KMKILELPFASGDLSMLVLLPDEVSDLERIEKTINFEKLTEWTNPNTMEKRRVKVYLPQMKIEEKYNLTS";
sequences[2] =
"VLMALGMTDLFIPSANLTGISSAESLKISQAVHGAFMELSEDGIEMAGSTGVIEDIKHSPESEQFRADHP";

File elementMassFile = new File("./src/main/resources/ElementMass.xml");
File aminoAcidCompositionFile = new
File("./src/main/resources/AminoAcidComposition.xml");
AminoAcidCompositionTable table =
PeptideProperties.obtainAminoAcidCompositionTable(elementMassFile,
aminoAcidCompositionFile);

//The difference between this example and short example 2 is that the
elementMassFile and aminoAcidCompositionFile will be only parsed once
//and stored in AminoAcidCompositionTable for quick and easy reuse in
the computation of multiple sequences. for(String sequence:sequences){

`   System.out.println("Molecular Weight: " + PeptideProperties.getMolecularWeightBasedOnXML(sequence, table));`

} </java>

Short Example 4: Computing composition of protein sequence
----------------------------------------------------------

<java> String sequence =
"QIKDLLVSSSTDLDTTLVLVNAIYFKGMWKTAFNAEDTREMPFHVTKQESKPVQMMCMNNSFNVATLPAE";

//Enrichment of a specific amino acid type
System.out.println("Composition of A: " +
PeptideProperties.getEnrichment(sequence, "A"));

//Enrichment of a list of amino acid types Map<String, Double>
composition = PeptideProperties.getAACompositionString(sequence);
for(String aa:composition.keySet()){

`   System.out.println("Composition of " + aa + ": " + composition.get(aa));`

} </java>

Short Example 5: Computing of all other physico-chemical properties
-------------------------------------------------------------------

<java> String sequence =
"QIKDLLVSSSTDLDTTLVLVNAIYFKGMWKTAFNAEDTRECMPFHVTKQESKPVQMMCMNNSFNVATLPAE";

//Absorbance System.out.println("Absorbance (Cys Reduced): " +
PeptideProperties.getAbsorbance(sequence, true));
System.out.println("Absorbance (Cys Not Reduced): " +
PeptideProperties.getAbsorbance(sequence, false));

//Extinction Coefficient System.out.println("Extinction Coefficient (Cys
Reduced): " + PeptideProperties.getExtinctionCoefficient(sequence,
true)); System.out.println("Extinction Coefficient (Cys Not Reduced):
" + PeptideProperties.getExtinctionCoefficient(sequence, false));

//Instability Index System.out.println("Instability Index: " +
PeptideProperties.getInstabilityIndex(sequence));

//Apliphatic Index System.out.println("Apliphatic Index: " +
PeptideProperties.getApliphaticIndex(sequence));

//Average Hydropathy Value System.out.println("Average Hydropathy Value:
" + PeptideProperties.getAvgHydropathy(sequence));

//Isoelectric Point System.out.println("Isoelectric Point: " +
PeptideProperties.getIsoelectricPoint(sequence));

//Net Charge System.out.println("Net Charge at pH 7: " +
PeptideProperties.getNetCharge(sequence)); </java>