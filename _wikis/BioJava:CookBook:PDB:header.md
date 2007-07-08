---
title: BioJava:CookBook:PDB:header
---

### How can I access the header information of a PDB file?

<java>

`   public static void main (String[] args){`  
`       try {`  
`           `  
`           PDBFileReader pdbr = new PDBFileReader();          `  
`           pdbr.setPath("/path/to/your/PDB/");`  
`           `  
`           String pdbCode = "5pti";`  
`           `  
`           Structure struc = pdbr.getStructureById(pdbCode);`  
`         `  
`           Map m = struc.getHeader();`  
`                    `  
`           `  
`           Set keys = m.keySet();`  
`           Iterator iter = keys.iterator();`  
`           while (iter.hasNext()){`  
`               String key = (String) iter.next();`  
`               System.out.println(key +": " +  m.get(key));`  
`           }`  
`           `  
`           `  
`       } catch (Exception e){`  
`           e.printStackTrace();`  
`       }`  
`   }`

</java>

gives the following output:

    title: STRUCTURE OF BOVINE PANCREATIC TRYPSIN INHIBITOR. RESULTS OF JOINT NEUTRON AND X-RAY REFINEMENT OF CRYSTAL FORM /II$ 
    technique: NEUTRON DIFFRACTION, X-RAY DIFFRACTION 
    classification: PROTEINASE INHIBITOR (TRYPSIN)
    depDate: 05-OCT-84
    modDate: 11-NOV-03
    idCode: 5PTI
    resolution: 1.8