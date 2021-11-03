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
Parte del codigo de este practico fue tomado y modificado de https://tomjenkins.netlify.app/2020/09/21/r-popgen-getting-started/


# Actividad práctica
______

## Correr en GUI
1. Cargar libreria
```sh
library(adegenet)
library(poppr)
library(dplyr)
library(hierfstat)
library(reshape2)
library(ggplot2)
library(RColorBrewer)
library(scales)
library(vcfR)
library(tidyverse)
```
2. #load popmap and create a list with individual ID and sites
```sh
popmap<-read.table("popmap.txt", sep= "\t", stringsAsFactors = FALSE)
ind=as.character(popmap$V1) # individual ID
site = as.character(popmap$V2) # site ID
```
3. #load popmap and create a list with individual ID and sites
```sh
#load vcf and convert in genind
vcf <- vcfR::read.vcfR("llqSNPmapped.vcf")
genind <- vcfR2genind(vcf, ploidy=2, ind.names = ind, pop = site)
```

4. #Perform a PCA (principle components analysis) on the species data set.
```sh
# Replace missing data with the mean allele frequencies
x = tab(genind, NA.method = "mean")

# Perform PCA
pca1 = dudi.pca(x, scannf = FALSE, scale = FALSE, nf = 3)

# Analyse how much percent of genetic variance is explained by each axis
percent = pca1$eig/sum(pca1$eig)*100
barplot(percent, ylab = "Genetic variance explained by eigenvectors (%)", ylim = c(0,10),
        names.arg = round(percent, 1))
```

5. #Visualise PCA results.
```sh
# Create a data.frame containing individual coordinates
ind_coords = as.data.frame(pca1$li)

# Rename columns of dataframe
colnames(ind_coords) = c("Axis1","Axis2","Axis3")

# Add a column containing individuals
ind_coords$Ind = indNames(genind)

# Add a column with the site IDs
ind_coords$Site = genind$pop

# Calculate centroid (average) position for each population
centroid = aggregate(cbind(Axis1, Axis2, Axis3) ~ Site, data = ind_coords, FUN = mean)

# Add centroid coordinates to ind_coords dataframe
ind_coords = left_join(ind_coords, centroid, by = "Site", suffix = c("",".cen"))

# Define colour palette
cols = brewer.pal(nPop(genind), "Set1")

# Custom x and y labels
xlab = paste("Axis 1 (", format(round(percent[1], 1), nsmall=1)," %)", sep="")
ylab = paste("Axis 2 (", format(round(percent[2], 1), nsmall=1)," %)", sep="")

# Custom theme for ggplot2
ggtheme = theme(axis.text.y = element_text(colour="black", size=12),
                axis.text.x = element_text(colour="black", size=12),
                axis.title = element_text(colour="black", size=12),
                panel.border = element_rect(colour="black", fill=NA, size=1),
                panel.background = element_blank(),
                plot.title = element_text(hjust=0.5, size=15) 
)

# Scatter plot axis 1 vs. 2
ggplot(data = ind_coords, aes(x = Axis1, y = Axis2))+
  # points
  geom_point(aes(fill = Site), shape = 21, size = 3, show.legend = T)+
  # custom labels
  labs(x = xlab, y = ylab)+
  ggtitle("Llanquihue PCA")+
  # custom theme
  ggtheme

# Export plot
ggsave("Llanquihue_PCA.png", width = 12, height = 8, dpi = 600)
```







