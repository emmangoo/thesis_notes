1) Introduction

- Motivation (from project doc) 
    
- Research question/ goals (project doc) 
    
- Thesis outline (what will the thesis cover)
    

2) Background & related works

- Multi-omics outlier detection (explain FRASER, OUTRIDER, etc.)
    
- Cis- vs trans-regulatory effects (biological def)
    
- Copy number variants (AMP/ DUP/ HDEL def)
    
- RNA pol2 machinery & transcriptional dysreg
    
- (Epigenetic mod?)
    
- Statistical methods used
    

3) Data & Materials

- Explain data (n patients, cancer types)
    
- Modalities (each of the files I used)
    
- Reference database (explain how I made the atlas)
    
- (preprocessing pipelines → maybe not necessary because not very complicated)
    

4) Methodology

- Defining cis/ trans effects (in main.py)
    
- Defining hyper-outliers 
    
- Stats framework for burden-association (chromosome aware/unaware per-gene burden association, ZIP & two-part hurdle, covariate-adjusted GLM, permutation of gene sets for Pol2, whole-pathway with Jaccard index stuff)
    
- Per-cancer analysis
    
- Hypothesis-driven stuff (core/acc spliceosome, epigenetic mods, small variants)
    
- Software & reproducibility 
    

5) Results 

6) Discussion

- Compare to literature 
    

7) Conclusion