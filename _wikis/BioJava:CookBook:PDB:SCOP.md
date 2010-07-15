---
title: BioJava:CookBook:PDB:SCOP
---

The BioJava SCOP parser can

-   automatically download the SCOP release files (if they are not at a
    specified local directory)
-   parse the SCOP files
-   provides an API to access any level of the SCOP classification.

This example loads a superfamily from SCOP and aligns the first domain
in this family against all others. <java> public static void
main(String[] args){

`     String cacheLocation = "/tmp/";`

`     String pdbId = "4HHB";`  
`    `  
`     // download SCOP if required and load into memory`  
`     ScopInstallation scop = new ScopInstallation(cacheLocation);`

`     List`<ScopDomain>` domains = scop.getDomainsForPDB(pdbId);`

`     System.out.println(domains);`

`     List`<ScopDescription>` superfams = scop.getByCategory(ScopCategory.Superfamily);`

`     System.out.println("Total nr. of superfamilies:" + superfams.size());`

`     // configure where to load PDB files from and `  
`     // what information to load`  
`     AtomCache cache = new AtomCache(cacheLocation, true);      `  
`     FileParsingParameters fileparams = new FileParsingParameters() ;`  
`     fileparams.setAlignSeqRes(false);`  
`     fileparams.setLoadChemCompInfo(true);`  
`     fileparams.setParseSecStruc(false);`  
`     cache.setFileParsingParams(fileparams);`  
`     `  
`     // get the first superfamily`  
`     ScopDescription superfam1 = superfams.get(0);`  
`     System.out.println("First superfamily: " + superfam1);`  
`     `  
`     ScopNode node = scop.getScopNode(superfam1.getSunID());`  
`     System.out.println("scopNode for first superfamily:" + node);`  
`     `  
`     List`<ScopDomain>` doms4superfam1 = scop.getScopDomainsBySunid(superfam1.getSunID());`  
`     ScopDomain dom1 = doms4superfam1.get(0);`  
`     `  
`     // align the first domain against all others members of this superfamily`  
`     for ( int i = 1 ; i < doms4superfam1.size() ; i ++){`

`        ScopDomain dom2 = doms4superfam1.get(i);`  
`       `  
`        try {`  
`           Structure s1 = cache.getStructureForDomain(dom1);`  
`           Structure s2 = cache.getStructureForDomain(dom2);`  
`           `  
`           Atom[] ca1 = StructureTools.getAtomCAArray(s1);`  
`           Atom[] ca2 = StructureTools.getAtomCAArray(s2);`  
`           StructureAlignment ce = StructureAlignmentFactory.getAlgorithm(CeMain.algorithmName);`  
`           AFPChain afpChain = ce.align(ca1, ca2);`  
`           `  
`           //System.out.println(afpChain.toCE(ca1, ca2));`  
`           `  
`           //StructureAlignmentDisplay.display(afpChain, ca1, ca2);`  
`           `  
`           System.out.println(dom1.getScopId() + " vs. " + dom2.getScopId()+ " :" + afpChain.getProbability());`  
`           `  
`        } catch (Exception e){`  
`           e.printStackTrace();`  
`        }`  
`     }`

} </java>