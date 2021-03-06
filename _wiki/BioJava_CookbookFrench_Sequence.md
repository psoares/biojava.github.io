---
title: BioJava:CookbookFrench:Sequence
permalink: wiki/BioJava%3ACookbookFrench%3ASequence
---

Comment faire une Sequence à partir d'une chaîne de caractères ou créer une chaîne à partir d'une Sequence?
-----------------------------------------------------------------------------------------------------------

La plupart du temps, nous voyons les séquences biologiques représentés
comme des chaînes de caraactères, par exemple
"atgccgtggcatcgaggcatatagc". C'est une manière pratique de visualiser et
de représenter un polymère biologique plus complexe. BioJava utilise des
*SymbolLists* et des *Sequences* pour représenter ces polymères
biologiques sous la forme d'objets. Les *Sequences* prolongent les
*SymbolLists* et contiennent des méthodes supplémentaires pour stocker
des données comme le nom de la séquence et toute les caractéristiques
qu'elle peut contenir. Cependant, vous pouvez à toute fin pratique
considérez les *Sequences* comme des *SymbolList*.

A l'intérieur d'une *Sequence* ou d'une *SymbolList*, le polymère
lui-même n'est pas stocker sous la forme d'une chaîne de type *String*.
BioJava fait la différence entre la nature des différents résidus d'un
biopolymère en utilisant des objets *Symbol* provenant de différents
*Alphabets*. De cette manière, il est facile de dire qu'une séquence est
faite d'ADN ou d'ARN ou autre chose et que le symbol 'A' de l'ADN n'est
pas égal au symbole 'A' de l'ARN. Les détails de l'utilisation des
*Symbols*, *SymbolLists* et *Alphabets* sont décrits ici. L'élément
crucial est qu'il est nécessaire d'avoir une façon pour un programmeur
de convertir une chaîne de caractères facilement saisissable en objet
BioJava et vice versa. Pour ce faire, BioJava a des *Tokenizers* qui
peuvent lire une chaîne de caractères et en parcourir le contenu pour le
donner à un objet *Sequence* ou *SymbolList* de Biojava. Dans le cas de
l'ADN, de l'ARN ou d'une protéine, il est possible de le faire avec un
simple appel d'une seule méthode. L'appel utilise une méthode statique
des classes *DNATools*, *RNATools* ou *ProteinTools*.

### D'une chaîne à une *SymbolList*

```java import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class StringToSymbolList {

` public static void main(String[] args) {`  
`  `  
`   try {`  
`     // créer une SymbolList d'ADN à partir d'une chaîne`  
`     SymbolList dna = DNATools.createDNA("atcggtcggctta");`

`     // créer une SymbolList d'ARN à partir d'une chaîne`  
`     SymbolList rna = RNATools.createRNA("auugccuacauaggc");`

`     // créer une SymbolList de Protein à partir d'une chaîne`  
`     SymbolList aa = ProteinTools.createProtein("AGFAVENDSA");`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     // ce qui arrivera si un caractère d'une chaîne n'est pas`  
`     // un caractère accepté par l"IUB pour ce Symbol.`  
`     ex.printStackTrace();`  
`   }`  
`  `  
` }`

} ```

### D'une chaîne à une *Sequence*

```java import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class StringToSequence {

` public static void main(String[] args) {`

`   try {`  
`     // créer une séquence d'ADN du nom de dna_1`  
`     Sequence dna = DNATools.createDNASequence("atgctg", "dna_1");`

`     // créer une séquence d'ARN du nom de rna_1`  
`     Sequence rna = RNATools.createRNASequence("augcug", "rna_1");`

`     // créer une séquence de protéine du nom de prot_1`  
`     Sequence prot = ProteinTools.createProteinSequence("AFHS", "prot_1");`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     // une exception lancée si vous utilisés un symbol non-IUB`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```

### D'une *SymbolList* à une chaîne de caractères

Vous pouvez appeller la méthode **seqString()** sur une *SymbolList* ou
une *Sequence* pour obtenir la chaîne de caractères contenant la
séquence.

```java import org.biojava.bio.symbol.\*;

public class SymbolListToString {

` public static void main(String[] args) {`  
`   SymbolList sl = null;`  
`   `  
`   // mettre ici votre code afin d'instantier sl`  
`  `  
`   // convertir sl en chaîne de caractères`  
`   String s = sl.seqString();`  
` }`

} ```
