# Identificación de inversiones cromosómicas por PCA

por [Cristian B. Canales-Aguirre](https://www.researchgate.net/profile/Cristian-Canales-Aguirre)
______


Esta actividad tiene como objetivo entregar herramientas para identificar potenciales inversiones cromosomicas usando metodos indirectos. Inversiones cromosomicas pueden albergar alelos coadaptados dada la ausencia de recombinacion de individuos heteorcigotos. Generalmente las inversiones o regiones que determinan el sexo, inhiben la recombinación, lo que da lugar a un elevado Desequilibrio de Ligamiento (LD) y por lo tanto a la herencia de un haplotipo en bloque. Para identificar regiones cromosomicas con inversiones hay metodos directos e indirectos. Los Metodos Directos estan relacionados principalmente "minando" explcitamente los datos genomicos obenidos mediante diferentes aproximacion para reducir la complejidad del genoma (e.g. RADseq, ddRAD, etc.) y plataformas de secuenciación (e.g., illumina, Pacbio, etc.). Por otro lado, los Metodos Indirectos se basan principalmente en patrones de diferenciacion y LD.

En esta actividad utilizando paquetes de R tales como ADEGENET ([Jombart and Ahmed, 2011](https://doi.org/10.1093/bioinformatics/btr521)) revelaremos patrones de diferenciacion poblacional a nivel cromosómico usando un analisis de componentes principales (PCA). Adicionalmente, visualizaremos patrones de desequilibrio de ligamiento en cada cromosoma calculando el estadistico r<sup>2</sup> ([Hill and Robertson, 1968](https://link.springer.com/article/10.1007/BF01245622)) por cada par de loci usando el programa PLINK ([Purcell et al. 2007](https://doi.org/10.1086/519795)).
    
  
  ### :warning: Leer los siguientes articulos y descargar los programas que sean necesarios: :warning:

**ADEGENET**
>Jombart, T., & Ahmed, I. (2011). [adegenet 1.3-1: new tools for the analysis of genome-wide SNP data](https://doi.org/10.1093/bioinformatics/btr521). Bioinformatics, 27(21), 3070-3071.

**PLINK**

>Purcell, S., Neale, B., Todd-Brown, K., Thomas, L., Ferreira, M. A., Bender, D., ... & Sham, P. C. (2007). [PLINK: a tool set for whole-genome association and population-based linkage analyses](https://doi.org/10.1086/519795). The American Journal of Human Genetics, 81(3), 559-575. ([Descargar](https://www.cog-genomics.org/plink/))

**Lecturas**
>Wellenreuther, M., & Bernatchez, L. (2018). [Eco-evolutionary genomics of chromosomal inversions](https://doi.org/10.1016/j.tree.2018.04.002). Trends in ecology & evolution, 33(6), 427-440.

>Arostegui, M. C., Quinn, T. P., Seeb, L. W., Seeb, J. E., & McKinney, G. J. (2019). [Retention of a chromosomal inversion from an anadromous ancestor provides the genetic basis for alternative freshwater ecotypes in rainbow trout](https://doi.org/10.1111/mec.15037). Molecular Ecology, 28(6), 1412-1427.

>Mérot, C. (2020). [Making the most of population genomic data to understand the importance of chromosomal inversions for adaptation and speciation](https://doi.org/10.1111/mec.15500). Molecular Ecology, 29(14), 2513-2516.

>McKinney, G., McPhee, M. V., Pascal, C., Seeb, J. E., & Seeb, L. W. (2020). [Network analysis of linkage disequilibrium reveals genome architecture in chum salmon](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7202013/). G3: Genes, Genomes, Genetics, 10(5), 1553-1561.

>Mérot, C., Oomen, R. A., Tigano, A., & Wellenreuther, M. (2020). [A roadmap for understanding the evolutionary significance of structural genomic variation](https://doi.org/10.1016/j.tree.2020.03.002). Trends in Ecology & Evolution, 35(7), 561-572.


### :nerd_face: Información y datos :nerd_face:
Esta actividad práctica utilizará datos aún no publicados, donde el manuscrito esta actualmente en praparación. La especie utilizada es _Oncorhynchus mykiss_ (Trucha arcoíris) muestreada en tres localidades en el lago Llanquihue. Especificamente, se utilizan marcadores SNPs obtenidos desde RADseq.



# Actividad práctica
______

## Correr en GUI
1. Cargar libreria
```sh
library("adegenet")
library("adegenet")
library("adegenet")
library("adegenet")
```
2. Abrir interfaz gráfica
```sh
Geneland.GUI(lib.loc = NULL)
```
3. Habilitar opciones avanzadas (Figura 1)![image](https://user-images.githubusercontent.com/58198031/137951221-bd232bdd-c4e9-401a-92b5-b23a21ee3c55.png)

4. En la pestaña Data Files es necesario establecer el directorio donde se guardaran los resultados obtenidos y cada output generado por GENELAND. Para esto seleccione Output directory y seleccione la carpeta “Práctico Geneland”. Posteriormente incorpore su base de datos de coordenadas geográficas, para esto presione Coordinate file y seleccione el archivo **corr.txt**, que se encuentra en la carpeta “Práctico Geneland”. Paso siguiente es incorporar su base de datos de genotipos, para esto presione Codominant markers file y seleccione el archivo **gene.txt**, que se encuentra en la carpeta “Práctico Geneland” (Figura 2)![image](https://user-images.githubusercontent.com/58198031/137951687-75d04023-28c0-49bf-b7eb-24ad0e5be15d.png)






