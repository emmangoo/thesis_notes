
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

Rank-sum
- chromosome-aware CNV burden testing recovers plausible trans-driver genes 
- 996 FDR-significant genes with cohen's d >= 0.5, 73 genes annotated in COSMIC oncogenes/ TSG
- top 5 genes box plots
- testing TSFM collinearity with MDM2 and CDK4 shows very high collinearity but also that TSFM is still significant on its own => mention low TSFM \ CDK4 or CDK4 \ TSFM carriers

Zero-inflation of gene+protein overlap 
- rank-sum fails, ZIP fails to converge on ~1/3 of genes 
- two-part hurdle model recovers some plausible genes but all have very few carriers of course 

Spliceosome
- high impact variant subset analysis (Rebekas analysis recreation)
- pathway agnostic analysis reveals several significant pathways, mRNA minor splicing pathway as top result => show all significant pathways here 
- negative binomial instead of Poisson used in GLM due to outlier distribution

RNA pol II
- pol II gene set identified via reactome query => pathway name containing "Polymerase II", so this includes the central pol II genes as well as accessory genes
- tried deletion vs duplication burden, pol II subunits vs accessory genes burden, variant tiering (HDEL/ HIGH impact, DEL/ MODERATE, AMP/DUP/LOW/MODIFIER) => more informative but no real interesting results 
- separated underexpression from overexpression
- circularity control: removed Pol II genes from target variable
- show IRR plot
- per-oncotree code analysis which was mostly uninformative except uveal melanoma => for discussion this can be useful as it matches literature
- (maybe delete this) epigenetic factor GLM from paper 
- pathway-agnostic analysis: same as for CNV analysis, recovered CDK4/ CDK6 pathway as top result (all genes in this pathway are annotated oncogenes), show all other pathways from this analysis
- random permutation test (10k) to check whether any gene set of this size produces a significant result

---

## Discussion

Chromosome awareness and burden-based CNV analysis
- top genes include annotated oncogenes 
- top 5 genes all on chromosome 12 => coamplification via chromothripsis/ local structural rearrangements inflates testing results which is why it makes sense that we have these genes clustered together especially with the naive test
- however CDK4 is known to coamplify with other known oncogenes like MDM2 which are also close on chromosome 12 => this means TSFM COULD still be a true trans-driver, but especially in light of the small number of patients the significant p value I recovered isn't necessarily a true signal 
- maybe mention caveat: there could be some intra-chromosomal trans-acting variants, so the chromosome-aware stats test could actually remove some legitimate drivers, but I think that this is an acceptable risk especially since I want to filter out the mass of local effects => chromosome-awareness implementation is a spatial heuristic, not an exact biological modelling
- CDK4 is a canonical oncogene and a G1/ S cell cycle driver => clinical methods are known for CDK4 inhibition 
- AGAP2/ AGAP2-AS1 biomarkers of some cancers/ promotes cancer cell invasion 
- TSFM is the most ambiguous result, biologically it is plausible for this to be a trans-driver because it is a mitochondrial translation factor (partner of EF-Tu) => because of high collinearity this result is not a certainty, could still be a passenger effect 

Zero-inflated models/ gene+protein overlap outliers
- from UQCRH result: CNV raises probability of expression+protein overlap outliers, but not magnitude => could be a switch-like mechanism which is known in biochemistry => dysregulation doesn't necessarily scale with 'dosage' => this is a speculative interpretation 
- discuss more closely why the ZIP test failed 

Minor spliceosome
- there are not that many minor spliceosome-dependent introns
- genes containing these introns are enriched for certain categories like RNA processing, cell cycle control, and DNA repair 
- so functionally this makes sense for aberrations here to be present in cancer => low-redundancy, high-precision machinery is being disrupted 

RNA Pol II
- primary hypothesis was that the loss of core transcriptional machinery leads to a loss of global transcription and thus underexpression outliers
- important effect: Pol II underexpression could be a proxy for general underexpression or chromosomal instability => that is why I introduced all these covariates, the removal of Pol II genes from the target variable, and the random permutation test => of course this doesn't 100% rule out confounding effects 

Pathway analysis/ CDK4 result
- unbiased & hypothesis-free/ agnostic analysis got the same CDK4 signal retrieved via the per-gene analysis => substantiates both methods 
- connect to CDK4/6 literature
- interpret the other pathway results

---

## Conclusion 

- summarise the hypotheses introduced at the beginning & the discussion for each 
- mention limitations 
- overarching message: cis effects are insufficient as sole explanations for genomic aberrations in cancer, biologically sound & interpretable trans-acting variants are worth integrating into pipelines

---

## Outlook

- mirrored from presentation: functional validation, cancer lineage specific tests, replication on TCGA cohort

