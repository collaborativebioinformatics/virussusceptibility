> CMU / DNAnexus Hackathon, October 19-21, 2023

# virustrajectory

A Python pipeline to build a vector database from the CORD-19 dataset and query it for a specific context in search for relevant scientific articles.

## Introduction

This is a project from the CMU/DNAnexus 2023 Hackathon which concentrated on finding the correlation between COVID-19 susceptibility and chronic diseases (such as cancer, hypertension, or diabetes) using vector comparison inference. There is a growing number of scientific literature related to Covid-19 and innovative initialives are taken up to ask and answer complicate questions to fight the disease [1]. We built a vector databases out of the CORD-19 dataset [2] to provide improvement in performance, scalability and flexibility of searching for relevant articles to certain queries [3, 8].

We tested our pipeline on a subset of the CORD-19 dataset, as well as on the whole CORD-19 dataset. 

Moreover, as a proof of principle, we created our own vector database out of a small number of articles embedded with SPECTER and tested the relevant article retrieval.

## The aims

- To find out a set of conditions that make patients with chronic diseases more susceptible to Covid-19.
- Does this set of conditions vary between different chronic diseases?

## Workflow for CORD-19

<img width="359" alt="Screenshot 2023-10-21 at 17 49 40" src="https://github.com/collaborativebioinformatics/virustrajectory/assets/82537630/97d96101-acc6-4591-9f0e-3627fb5b87f0">

## Workflow for the custom dataset



## Methods

The jupyter notebooks have been put in the `scripts/` directory.

The CORD-19 dataset contains metadata and embeddings generated from articles related to Covid-19. We retrieved the embeddings with references to the original articles from the dataset. The embedding were generated with SPECTER (Scientific Paper Embeddings using Citation-informed TransformERs) [4]. SPECTER is a method to generate high-quality article representations. The training of the model and its implementation details can be found in the original article [4]. We created a vector database with 'insert', 'query', and 'retrieve' methods [9]. Then, we inserted the CORD-19 embedding into the vector database.

We downloaded SPECTER from GitHub (https://github.com/allenai/specter) and used it to create an embedding for the example query ("What combinations of features predispose cohorts to virus susceptibility?"). Then, we compare the embedding of this query with all the embeddings in the dataset and rank the comparisons according to cosine similarity. The best-ranked paper thus retrieved should be the closest to our query in terms of the context (it should have the highest cosine similarity measure).


> Remark: Cosine similarity turned out to be not suitable for high-dimensional vector comparison. For this reason we reduced the dimensionality of vectors with random projection [5, 6] -- specifically Gaussian random projection [7]. Then we used cosine similarity to search for articles that would be the most relevant to the query.

As a proof of principle we created a dataset of small number of articles (1000) and embedded them with SPECTER. Then we inserted the embeddings into a vector database. We tested the retrieval of most relavant articles. The workflow can be found here: `scripts/query_custom_dataset.ipynb`.

## Initial, naive ideas-

- Firstly, we were trying to do virus trajectory inference with the purpose of finding the change in trajectory due to COVID, but we couldnt find any longitudinal data with COVID patients, so had to change plans slightly.
- We were then planning to filter all the papers with a particular word (like 'hypertension') and then out of all the resultant papers, we would rank the words appearing in them by frequency. Using this, we could establish correlation between pairs of words/lists. In this case, the words would lack context, so we didn't go this route. 

## Results

- Building a vector database out of the CORD-19 dataset and storing it in a pickle file reduced the size from 15 GB to 5 GB.
- Querying the vector database with the embedded query takes ~18 sec; with the query embedded and treated with random projectrion ~6sec.
- reproduciblity

### example query for CORD-19

<img width="444" alt="Screenshot 2023-10-21 at 17 01 00" src="https://github.com/collaborativebioinformatics/virustrajectory/assets/82537630/a62abb14-656b-4b7d-b505-e8eb694d3f62">

### example result for CORD-19

<img width="519" alt="Screenshot 2023-10-21 at 16 56 49" src="https://github.com/collaborativebioinformatics/virustrajectory/assets/82537630/bdd7d566-3b70-452a-b932-4fd0e0bbf8df">


<img width="515" alt="Screenshot 2023-10-21 at 17 02 19" src="https://github.com/collaborativebioinformatics/virustrajectory/assets/82537630/1675736b-851d-4a5e-960b-a01596a0c979">

### example result for custom dataset

### example result for custom dataset

## Acknowledgments

The Hackathon was organized at the [Carnegie Mellon Libraries](https://www.cmu.edu).

[DNAnexus](dnanexus.com) provided computing resources for this project.

### Thank you to the Organizers of the CMU / DNAnexus Hackathon 2023!

## Bibliography
1. Lucy Lu Wang, Kyle Lo, Text mining approaches for dealing with the rapidly expanding literature on COVID-19, Briefings in Bioinformatics, Volume 22, Issue 2, March 2021, Pages 781–799, https://doi.org/10.1093/bib/bbaa296
2. Wang LL, Lo K, Chandrasekhar Y, Reas R, Yang J, Burdick D, Eide D, Funk K, Katsis Y, Kinney R, Li Y, Liu Z, Merrill W, Mooney P, Murdick D, Rishi D, Sheehan J, Shen Z, Stilson B, Wade AD, Wang K, Wang NXR, Wilhelm C, Xie B, Raymond D, Weld DS, Etzioni O, Kohlmeier S. CORD-19: The Covid-19 Open Research Dataset. ArXiv [Preprint]. 2020 Apr 22:arXiv:2004.10706v4. PMID: 32510522; PMCID: PMC7251955.
3. https://www.pinecone.io/learn/vector-database/
4. SPECTER: https://arxiv.org/abs/2004.07180
5. Random projection: http://people.ee.duke.edu/~lcarin/p93.pdf
6. https://towardsdatascience.com/random-projection-in-python-705883a19e48
7. Gaussian random projection: https://scikit-learn.org/stable/modules/generated/sklearn.random_projection.GaussianRandomProjection.html
8. https://learn.microsoft.com/en-us/semantic-kernel/memories/vector-db
9. https://www.linkedin.com/pulse/vector-databases-demystified-part-2-building-your-own-adie-kaye/


## Relevant literature

### Covid
1. He, Y., Yu, H., Ong, E. et al. CIDO, a community-based ontology for coronavirus disease knowledge and data integration, sharing, and analysis. Sci Data 7, 181 (2020). https://doi.org/10.1038/s41597-020-0523-6
2. . Sharma, S., Jain, S. CovidO: an ontology for COVID-19 metadata. J Supercomput (2023). https://doi.org/10.1007/s11227-023-05509-4
3. . Astghik Sargsyan, Alpha Tom Kodamullil, Shounak Baksi, Johannes Darms, Sumit Madan, Stephan Gebel, Oliver Keminer, Geena Mariya Jose, Helena Balabin, Lauren Nicole DeLong, Manfred Kohler, Marc Jacobs, Martin Hofmann-Apitius, The COVID-19 Ontology, Bioinformatics, Volume 36, Issue 24, December 2020, Pages 5703–5705, https://doi.org/10.1093/bioinformatics/btaa1057
4. . Qingyu Chen, Alexis Allot, Zhiyong Lu, LitCovid: an open database of COVID-19 literature, Nucleic Acids Research, Volume 49, Issue D1, 8 January 2021, Pages D1534–D1540, https://doi.org/10.1093/nar/gkaa952
5. . Dutta, B. and DeBellis, M. (2020). CODO: an ontology for collection and analysis of COVID-19 data. Accepted for publication in the Proc. of 12th Int. Conf. on Knowledge Engineering and Ontology Development (KEOD), 2-4 November 2020, https://doi.org/10.48550/arXiv.2009.01210
### Vector comparison
6. E. D. Madiga and S. Iloga, "Enhancing Vector Comparison Using HMMs," in IEEE Access, vol. 11, pp. 96939-96953, 2023, doi: 10.1109/ACCESS.2023.3312019
### Vector databases
7. https://learn.microsoft.com/en-us/semantic-kernel/memories/vector-db
8. https://www.linkedin.com/pulse/vector-databases-demystified-part-2-building-your-own-adie-kaye/
### Disease trajectory analysis
9. William D. Rooney, Yosef A. Berlow, William T. Triplett, Sean C. Forbes, Rebecca J. Willcocks, Dah-Jyuu Wang, Ishu Arpan, Harneet Arora, Claudia Senesac, Donovan J. Lott, Gihan Tennekoon, Richard Finkel, Barry S. Russman, Erika L. Finanger, Saptarshi Chakraborty, Elliott O'Brien, Brendan Moloney, Alison Barnard, H. Lee Sweeney, Michael J. Daniels, Glenn A. Walter, Krista Vandenborne, Neurology Apr 2020, 94 (15) e1622-e1633; DOI: 10.1212/WNL.0000000000009244
10. I Delor, J-E Charoin, R Gieschke, S Retout, P Jacqmin, Modeling Alzheimer's Disease Progression Using Disease Onset Time and Disease Trajectory Concepts Applied to CDR-SOB Scores From ADNI, https://doi.org/10.1038/psp.2013.54
