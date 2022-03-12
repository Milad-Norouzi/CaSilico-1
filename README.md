# CaSilico R Package

# Introduction

The efficiency of CRISPR-Cas system is highly depends on well-designed CRISPR RNA (crRNA). To facilitate the use of various types of CRISPR-Cas systems by a wide range of researchers, there is a need for development of computational tools to design crRNAs which cover different CRISPR-Cas systems with off-target analysis capability. Numerous crRNA design tools have been developed but nearly all of them are dedicated to design crRNA for genome editing. 


Hence, we developed a tool matching the needs of both beginners and experts, named Casilico, which was inspired by the limitations of the current gRNA design tools for designing crRNAs for Cas12, Cas13, and Cas14 CRISPR-Cas systems. Using a list of important features such as mismatch tolerance rules, self-complementarity, GC content, frequency of cleaving base around the target site, target accessibility and PFS (protospacer flanking site) or PAM (protospacer adjacent motif) requirement, Casilico searches all potential crRNAs in a user-input sequence. Considering these features help users to rank all crRNAs for a sequence and make an informed decision about whether a crRNA is suited for an experiment or not. Our tool is sufficiently flexible to tune some key parameters governing the design of crRNA and identification of off-targets, which can be led to increases the chances of successful CRISPR-Cas experiments.

Casilico outperforms previous crRNA design tools in the following respects: 1) supporting any reference genome/transcriptome for which a FASTA file is available; 2) designing crRNAs that simultaneously target multiple sequences through conserved region detection among a set of sequences; 3) considering new CRISPR-Cas subtypes; 4) reporting a list of different features for each candidate crRNA, which can help the user to select the best one. Given these capabilities, Casilico addresses end-user concerns arising from the use of sophisticated bioinformatics algorithms and has a wide range of potential research applications in different areas especially design of crRNA for pathogen diagnosis. 

Casilico was successfully applied to design crRNAs for different genes in SARS-CoV-2 genome, as some of the crRNAs have been experimentally tested in the previous studies.

![ش](https://user-images.githubusercontent.com/9910942/157799363-8f890ee4-4003-41f7-959c-d323b1bbeaab.png)

Casilico workflow. (A) Casilico accepts a single or a set of DNA or RNA sequences to be scanned for crRNA designing. (B) When more than one sequences is given as input, the conserved regions among them automatically detect considering conservation threshold and one of the two different approaches for identifying conserved regions. (C) A sliding window (stride of 1 nt) is employed across the single sequences or conserved region of multiple sequences to specify potentail target sites. (D) Casilico applies multiple criteria for crRNA designing, performs off-target analysis and returns outputs in an interactive graphical interface and some files such as MSA and secondary structure (E & F).





# Installation

```
library("devtools")

install_github("mrb20045/CaSilico")
```



# A quick example to use CaSilico package
```
library("CaSilico")


#Run with fasta_file_location

data<-paste0(system.file(package = "CaSilico"),"/data/3D.fasta")
CaSilico(Results_folder_name="Example",
         fasta_file_location=data,
         Accession_Number=NULL,
         CRISPR_Types=c("casVI_A"),
         method = 1,
         mismatch_threshold=0.98,
         off_Target = F,
         ask_question = F)




#Run with fasta_file_location and off-target prediction

data<-paste0(system.file(package = "CaSilico"),"/data/3D.fasta")

genome_dir<-paste0(system.file(package = "CaSilico"),"/dependency/genomes_off_target")

location_of_off_target_sequene_file=file.path(genome_dir,list.files(genome_dir))

name_of_off_target_sequence_file=c("Genome1","Genome2","Genome3")

CaSilico(Results_folder_name="Example2",
         fasta_file_location=data,
         Accession_Number=NULL,
         CRISPR_Types=c("casVI_A","casVI_B","casVI_D","casV_A","casV_B","casV_F1"),
         method = 1,
         mismatch_threshold=0.98,
         off_Target = T,
         ask_question = F,
         Organism=NULL,
         local_file_for_off_target=T,
         location_of_off_target_sequene_file=location_of_off_target_sequene_file,
         name_of_off_target_sequence_file=name_of_off_target_sequence_file)




 #Run with fasta_file_location

 CaSilico(Results_folder_name="Example3",
          Accession_Number=c("U15717", "U15718"),
          CRISPR_Types=c("casVI_A","casVI_B"),
          method = 1,
          mismatch_threshold=0.98,
          off_Target = F,
          ask_question = F)




 #Run with coordinate
 CaSilico(Results_folder_name="Example4",
          seq_cordinate=list(chromosome=c("1","1"),
                             start=c("2000","2000"),
                             end=c("2150","2150"),
                             strand=c("-","-"),
                             species = c("bos_taurus","bos_taurus")),
          CRISPR_Types=c("casVI_B","casVI_A"),
          method = 1,
          mismatch_threshold=0.98,
          off_Target = F,
          ask_question = F)



```

# License
GPL-3
