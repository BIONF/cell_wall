# Data for pPCD analysis

- *coreTaxa_dir*, *searchTaxa_dir* and *annotation_dir* contain data for 18.648 refseq taxa used for the ortholog search. Most of them were obtained from our local data repository at `/share/gluster/GeneSets/NCBI-Genomes/`.

- *pHMMs* folder contains the compiled core ortholog groups along with their profile HMMs for the final ortholog searches

- The seed proteins are located in the *seed_genes* folder, organized into subfolders named after their corresponding reference species - the species from which the sequences was derived

- `all_taxa.txt` lists all the taxa IDs (in BIONF format)

- In the *scripts* folder, you will find the *id2family_mapping.txt* file, which maps the seed protein IDs with their corresponding enzyme family. For example, GH75_UKZ55717.1 indicates that protein UKZ55717.1 belongs to the GH75 family.

# How to perform fDOG search

To run fDOG, you need to specify:

- `--seqFile` a single fasta file of the seed protein
- `--jobName` name of the output files and folders
- `--refspec` the corresponding reference species in BIONF format
- `--corepath`, `--searchpath`, `--annopath` paths to *coreTaxa_dir*, *searchTaxa_dir* and *annotation_dir*
- `--featureFile` parameter specifies the annotation tools used for the FAS calculation (please see [https://github.com/BIONF/FAS/wiki/Annotation](https://github.com/BIONF/FAS/wiki/Annotation))
- `--outpath` output path
- `--cpus` number of CPUs
- `--notAddingTaxa` (optional) taxa that don't have any ortholog will not be added into the final phylogenetic profile output

For example:

```
fdog.run --seqFile seed_genes/LICRA@688394@GCA_000945115_1/CDS07538.1.fa --jobName CDS07538.1 --refspec LICRA@688394@000945115_1 --maxDist phylum --corepath coreTaxa_dir --searchpath searchTaxa_dir --annopath annotation_dir --featureFile annoTools.txt --outpath ./ --cpus 8 --notAddingTaxa
```

We provide an example for running fDOG for the seed proteins of *Rhizoctonia solani* using a SLURM cluster at `/scripts/run_fdog.sh`.
