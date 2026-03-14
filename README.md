# 2nd_IGIB-ICMR_Workshop
1. Introduction to Core Unix Utilities
2. Introduction to Shell & BASH Scripting
3. Package Manager (Conda)
4. Bioinformatics Tools (seqkit, seqtk) 
---
```bash
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/021/613/535/GCA_021613535.1_ASM2161353v1/GCA_021613535.1_ASM2161353v1_genomic.fna.gz
```
---
## grep

`grep` (Global Regular Expression Print) is a command-line utility used to search for text patterns within files or data streams. It implements regular expression (regex) pattern matching, making it a powerful tool in data processing pipelines, log analysis, and bioinformatics workflows.

### Example

```bash
grep "pattern" filename.txt
```

### Decompress `.gz` files

```bash
gunzip *.gz
```
