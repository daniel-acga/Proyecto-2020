---
title: "Results_RADSeqMicronbiome"
author: "Daniel E Acosta"
date: "26/7/2020"
output:
  pdf_document: default
  html_document: default
---

```{r, include=FALSE, echo=FALSE}

library(ggplot2)
library(dplyr)


tax <- read.table("../data/GrossmaniaRef_97_tax.txt", header= TRUE, sep = "")
tax$V1 <- "GRef_97"


tax1  <- read.table("../data/DPond_97_tax.txt", header= TRUE, sep = "")
tax1$V1 <- "DPond_97"

tax2 <-  read.table("../data/DPond_95_tax.txt", header= TRUE, sep = "")
tax2$V1 <- "DPond_95"

tax3 <- read.table("../data/DendroDenovo_97_tax.txt", header= TRUE, sep = "")
tax3$V1 <- "Denovo_97"


tax4  <- read.table("../data/DendroDenovo_95_tax.txt", header= TRUE, sep = "")
tax4$V1 <- "Denovo_95"

tax5 <-  read.table("../data/DendroRef_97_tax.txt", header= TRUE, sep = "")
tax5$V1 <- "DRef_97"

taxx <- bind_rows(tax, tax1, tax2, tax3, tax4, tax5)

taxx_x <- taxx[!(taxx$V3 == "Arthropoda"| taxx$V3 == "Chordata" | taxx$V3 == "Echinodermata"| taxx$V3 == "Mollusca" | taxx$V3 == "Porifera" | taxx$V3 == "Platyhelminthes" | taxx$V3 == "Streptophyta"| taxx$V3 == "multiple"),]

a <-ggplot(taxx, aes (x = V1)) + geom_bar(aes(fill=V3)) +
  labs(x= "phylum", y="no seqs") + theme_minimal() 


b <-ggplot(taxx_x, aes (x = V1)) + geom_bar(aes(fill=V3) ) +
  labs(x= "phylum", y="no seqs") + theme_minimal() 

```


# RADSeq Microbiome Results
The majority of the sequences found matched with *Arthropoda* database references, but also another seven problematic phyla were present and filtered. 

**Table 1: Total matches with 90% similirity**

```{r, echo =FALSE, comment=NA}
o <- table(taxx$V1, taxx$V3)
o

a + theme(legend.title = element_blank()) + ggtitle ("Total matches, 90% similirity") 

```

Overall, the most commun phyla found were *Ascomycota* and *Proteobacteria*. Furthermore the most promising assembly method used in this survey was the use of an insect reference genome as filter on the subset of of the reference specie samples (*Dendroctonus ponderosae*) with a clustering threeshold of 95%.


**Table 2: Filtered matches with 90% similirity**

```{r, echo =FALSE, comment=NA}

p <- table(taxx_x$V1, taxx_x$V3)
p

b + theme(legend.title = element_blank()) + ggtitle ("Filtered matches, 90% similirity") 


```