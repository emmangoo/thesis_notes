
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



