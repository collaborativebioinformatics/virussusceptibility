> CMU / DNAnexus Hackathon 2023

# virustrajectory

## Introduction

This is a project from the CMU/DNAnexus 2023 Hackathon, in which we are trying to find the correlation of COVID-19 susceptibility with chronic diseases (such as cancer, hypertension or diabetes), using vector trajectory inference.

We developed a Python pipeline to create vector database and query it for a specific context in relevant scientific articles.

Embeddings are high-dimensional vectors that facilitate searching for similar context in 

Vector databases allow for performance, scalability, and flexibility when working with embeddings.

We tested our pipeline on a subset of the CORD-19 dataset. 

## The aim

- To find out the set of conditions that make patients with chronic diseases more susceptible to COVID, for a given chronic disease
- How does this set of conditions vary between different chronic diseases?

## Workflow

<img width="462" alt="Screenshot 2023-10-19 at 2 50 06 PM" src="https://github.com/collaborativebioinformatics/virustrajectory/assets/72993520/089f13fe-8ce9-4e5e-9d09-ea611960a5f3">

## Methods

CORD-19 dataset: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7251955/

The dataset contains metadata and embeddings generated from the articles with SPECTER (Scientific Paper Embeddings using Citation-informed TransformERs) (https://arxiv.org/pdf/2004.07180.pdf ; https://github.com/allenai/specter). SPECTER is a method to generate high-quality article representations. The training and implementation details can be found here: https://arxiv.org/pdf/2004.07180.pdf.

VectorDB: https://jina.ai/news/vectordb-a-python-vector-database-you-just-need-no-more-no-less/

We retrieved the embeddings with references to the orginal articles from the CORD-19 dataset.

We created a vector database with insert, query and retrieve methods.

We used SPECTER to create an embedding for the example query ("").

## Literature

### KG
1. Benjamin J. Stear, Taha Mohseni Ahooyi, Shubha Vasisht, Alan Simmons, Katherine Beigel, Tiffany J. Callahan, Jonathan C. Silverstein, Deanne M. Taylor
bioRxiv 2023.02.11.528088; doi: https://doi.org/10.1101/2023.02.11.528088
2. Silva, M.C.; Eugénio, P.; Faria, D.; Pesquita, C. Ontologies and Knowledge Graphs in Oncology Research. Cancers 2022, 14, 1906. https://doi.org/10.3390/ cancers14081906
### Covid
3. He, Y., Yu, H., Ong, E. et al. CIDO, a community-based ontology for coronavirus disease knowledge and data integration, sharing, and analysis. Sci Data 7, 181 (2020). https://doi.org/10.1038/s41597-020-0523-6
4. Sharma, S., Jain, S. CovidO: an ontology for COVID-19 metadata. J Supercomput (2023). https://doi.org/10.1007/s11227-023-05509-4
5. Astghik Sargsyan, Alpha Tom Kodamullil, Shounak Baksi, Johannes Darms, Sumit Madan, Stephan Gebel, Oliver Keminer, Geena Mariya Jose, Helena Balabin, Lauren Nicole DeLong, Manfred Kohler, Marc Jacobs, Martin Hofmann-Apitius, The COVID-19 Ontology, Bioinformatics, Volume 36, Issue 24, December 2020, Pages 5703–5705, https://doi.org/10.1093/bioinformatics/btaa1057
6. Qingyu Chen, Alexis Allot, Zhiyong Lu, LitCovid: an open database of COVID-19 literature, Nucleic Acids Research, Volume 49, Issue D1, 8 January 2021, Pages D1534–D1540, https://doi.org/10.1093/nar/gkaa952
7. Dutta, B. and DeBellis, M. (2020). CODO: an ontology for collection and analysis of COVID-19 data. Accepted for publication in the Proc. of 12th Int. Conf. on Knowledge Engineering and Ontology Development (KEOD), 2-4 November 2020, https://doi.org/10.48550/arXiv.2009.01210
### Vector comparison
8. E. D. Madiga and S. Iloga, "Enhancing Vector Comparison Using HMMs," in IEEE Access, vol. 11, pp. 96939-96953, 2023, doi: 10.1109/ACCESS.2023.3312019
### Vector dbs
9. https://learn.microsoft.com/en-us/semantic-kernel/memories/vector-db
10. https://www.linkedin.com/pulse/vector-databases-demystified-part-2-building-your-own-adie-kaye/
### Disease trajectory analysis
11. William D. Rooney, Yosef A. Berlow, William T. Triplett, Sean C. Forbes, Rebecca J. Willcocks, Dah-Jyuu Wang, Ishu Arpan, Harneet Arora, Claudia Senesac, Donovan J. Lott, Gihan Tennekoon, Richard Finkel, Barry S. Russman, Erika L. Finanger, Saptarshi Chakraborty, Elliott O'Brien, Brendan Moloney, Alison Barnard, H. Lee Sweeney, Michael J. Daniels, Glenn A. Walter, Krista Vandenborne
Neurology Apr 2020, 94 (15) e1622-e1633; DOI: 10.1212/WNL.0000000000009244
11. I Delor, J-E Charoin, R Gieschke, S Retout, P Jacqmin, Modeling Alzheimer's Disease Progression Using Disease Onset Time and Disease Trajectory Concepts Applied to CDR-SOB Scores From ADNI, https://doi.org/10.1038/psp.2013.54
