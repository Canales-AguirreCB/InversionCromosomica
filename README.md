# Identificación de inversiones cromosómicas por PCA

por [Cristian B. Canales-Aguirre](https://www.researchgate.net/profile/Cristian-Canales-Aguirre)
______


Esta actividad tiene como objetivo entregar herramientas para identificar potenciales inversiones cromosomicas usando metodos indirectos. Inversiones cromosomicas pueden albergar alelos coadaptados dada la ausencia de recombinacion de individuos heteorcigotos. Generalmente las inversiones o regiones que determinan el sexo, inhiben la recombinación, lo que da lugar a un elevado Desequilibrio de Ligamiento (LD) y por lo tanto a la herencia de un haplotipo en bloque. Para identificar regiones cromosomicas con inversiones hay metodos directos e indirectos. Los Metodos Directos estan relacionados principalmente "minando" explcitamente los datos genomicos obenidos mediante diferentes aproximacion para reducir la complejidad del genoma (e.g. RADseq, ddRAD, etc.) y plataformas de secuenciación (e.g., illumina, Pacbio, etc.). Por otro lado, los Metodos Indirectos se basan principalmente en patrones de diferenciacion y LD.

En esta actividad utilizando paquetes de R tales como ADEGENET ([Jombart and Ahmed, 2011](https://doi.org/10.1093/bioinformatics/btr521)) revelaremos patrones de diferenciacion poblacional a nivel cromosómico usando un analisis de componentes principales (PCA). Adicionalmente, visualizaremos patrones de desequilibrio de ligamiento en cada cromosoma calculando el estadistico r<sup>2</sup> ([Hill and Robertson, 1968](https://link.springer.com/article/10.1007/BF01245622)) por cada par de loci usando el programa PLINK ([Purcell et al. 2007](https://doi.org/10.1086/519795)).
    
  
  ### :warning: Previo a realizar esta actividad, leer los siguientes articulos y descargar los que sean necesarios: :warning:

**Primer-BLAST**

>Ye, J., Coulouris, G., Zaretskaya, I., Cutcutache, I., Rozen, S., & Madden, T.L. (2012). [Primer-BLAST: a tool to design target-specific primers for polymerase chain reaction](https://bmcbioinformatics.biomedcentral.com/track/pdf/10.1186/1471-2105-13-134.pdf). BMC Bioinformatics, 13(1), 1-11. 

**MSATCOMMANDER**

>Faircloth, B.C. (2008). [MSATCOMMANDER: Detection of microsatellite repeat arrays and automated, locus‐specific primer design](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.720.2181&rep=rep1&type=pdf). Molecular Ecology Resources, 8(1), 92-94. ([Descargar](https://code.google.com/archive/p/msatcommander/downloads))
