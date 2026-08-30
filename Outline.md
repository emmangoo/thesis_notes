
---

## Title / Abstract

Investigating Trans-Regulatory Effects using Multi-Omics Outliers in Cancer

Abstract:
- local/ cis explanations can't explain all multi-omic aberrations/ outliers in cancer
- hypothesis is that trans-acting variants can cause disruption on a large scale (CNVs, spliceosome, RNA Pol II)
- outline pan-cancer cohort, annotated with OUTRIDER/ FRASER/ PROTRIDER
- brief results overview 

---

## Introduction

Motivation:
	Outliers in genes attributed to local genetic changes can be classified as cis-acting variants. These variants constitute the main focus of standard multi-omic outlier detection analyses. While cis-effect detection remains paramount to rare diseases, pan-cancer cohorts demonstrate a far higher baseline mutational burden. While most cancer patients have 10 or fewer molecular outliers, a few 'hyper-outlier' samples exhibit disorder on a much larger scale. These hyper-outliers cannot be explained only by cis effects or an accumulation of independent local hits. Singular hits to global regulators can explain the systemic failure of multiple downstream targets. Identifying these trans-acting variants can thus identify singular targets for novel cancer therapies. In cancer genomics, passenger and silent mutations are well-documented, highlighting the need for the separation of causal and non-causal variants.
	This thesis aims to separate cis- from trans-effects, revealing singular variants that drive genome-wide outliers, and quantifying how much of the hyper-outlier phenomenon can be explained by trans-regulatory failure.

Introduction to using the multi-omic approach/ focusing on RNAseq
- combining DNAseq with RNAseq is useful, "RNA-seq can help to reveal splicing defects, the  48 mono-allelic expression of heterozygous loss-of-function variants, and expression outliers" (OUTRIDER) 
- looking at noncoding genes in addition to coding genes is useful => "implies that noncoding variants account for roughly one in five cases" 
- => this the reason for using multi-omic data + all genes/ not just coding genes

Aims/ hypotheses/ target questions (not sure if this section is necessary)
- CNV question (do CNVs in genes act as trans-regulators and is it possible to find real drivers amidst passenger effects)
- spliceosome (does disruption of core spliceosomal machinery increase splicing outlier burden)
- RNA Pol II (do defects drive transcriptional dysregulation independently of CNVs and cancer lineage)

---

## Background & Related works

Cis vs trans effects 
- structural variants (deletion/ amplification) can explain local expression changes
- trans effects are harder to interpret/ identify than local cis effects
- maybe find a proper widely-accepted definition of trans effects?

Current outlier calling methods
- explain outrider
- explain fraser
- explain protrider

CNVs & Structural changes
- explain passenger vs driver genes conceptually & why naive burden testing isn't the best
- explain chromothripsis & how it leads to structural linkage of neighbouring genes 
- CDK4 amplicon

Cancer genes
- define oncogene, TSG
- inheritance patterns of cancer genes => useful to have a germline & somatic analysis
- different cancer types have very different baseline/ expected burdens for differing outlier types 

Splicing
- some splicing factors are known oncogenes, eg SF3B1 => existing linkage to changes in splicing patterns in several cancer subtypes, eg uveal melanoma 
- uveal melanoma is one of the few cancer types where overexpression burden is associated with higher total outlier burden
- explain the minor spliceosome/ minor splicing pathway (how many introns, known disease associations)
- rarity != causality for rare variants but single cases do matter => LRP1B example? + TP53 isoforms example for CML

RNA Pol II and transcriptional dysregulation
- Pol II dysfunction known in cancer (eg POL2RA/B mutation or POL2RA deletion with TP53)
- transcriptional machinery as an oncogenic mechanism 
- maybe mention epigenetic factors paper for transcriptional dysregulation
- CDK4/CDK6 explanation

Additional motivation
- CUP as an example of why multi-omic/ system-level analysis matters
- when molecularly-informed therapy is applied median overall survival increases
- analysis of CUP patients reveals genetic heterogeneity and frequent alterations in known oncogenes

---

## Data & methods

Cohort 
- pan cancer, 3559 patients, etc (overall stats)
- maybe explain here or later: many cohorts are very small so for a lot of the analysis a minimum carrier threshold was applied both for genes and cohorts 

Database
- maybe explain database creation in short paragraph? reactome + ensembl + cosmic data collated into reference database used throughout for pathway/ gene/ chromosome/ etc information

Data prep
- gene ID => gene symbol mapping via database 
- chromosome mapping via database (ensembl info) if not available directly in data
- deduplication to compute carrier status per patient

Burden definitions
- per-sample per-omic burden = count of unique outlier genes for that sample 
- gene + protein overlap burden = genes that are simultaneously an expression outlier and a protein outlier in the same sample (maybe mention this here already to set up zero-inflation sample)
- chromosome-count matrices: per-sample per-chromosome outlier counts 

Statistical framework => is this good/ necessary/ unnecessary? 
- Global rank-sum with FDR: carriers of CNV or outlier in gene X ranked against global burden distribution, standard rank-sum formula applies
- Chromosome-aware version of the same test: subtract outliers on the same chromosome as current gene of interest from a sample's total burden with the aim of removing local/ passenger effects
- Cohen's d: filtered top FDR significant genes by cohen's d >= 0.5 to include only genes with meaningful effect size
- Zero-inflated Poisson: used for sparse data, but Hessian-inversion warnings + ~1/3 of genes not converging led to this being a bad method/ not useful in the end, but maybe good to mention as method nonetheless? 
- Two-part hurdle model: consists of logistic regression (binary, asking if there is an outlier at all) and truncated Poisson (magnitude of outlier given that it is present) components => this is better than ZIP for this case 
- Negative binomial GLM: diagnosis, background CNV burden included as covariates, HC3 robust errors used  
- Pathway-agnostic analysis: 2267 reactome-annotated pathways, built a per-pathway carrier vs burden GLM
	- gene set size filter 5-200 genes
	- carrier-frequency filter min 5 max 15%
	- FDR correction
	- Jaccard hierarchical clustering with distance threshold 0.5
- collinearity check for TSFM/ CDK4/ MDM2 to interpret chr12 results 

Software/ packages & code availability
- do i need to document the version of each package?
- link github repo

---

## Results



