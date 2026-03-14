# 2nd_IGIB-ICMR_Workshop
1. Introduction to Core Unix Utilities
2. Introduction to Shell & BASH Scripting
3. Package Manager (Conda)
4. Bioinformatics Tools (seqkit, seqtk) 
---
### Sample file 1
```bash
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/021/613/535/GCA_021613535.1_ASM2161353v1/GCA_021613535.1_ASM2161353v1_genomic.fna.gz
```
#### Decompress `.gz` files

```bash
gunzip *.gz
```
---
### grep

`grep` (Global Regular Expression Print) is a command-line utility used to search for text patterns within files or data streams. It implements regular expression (regex) pattern matching, making it a powerful tool in data processing pipelines, log analysis, and bioinformatics workflows.

#### Example

```bash
grep "pattern" filename.txt
```

#### Rename a File
```bash
mv GCA_021613535.1_ASM2161353v1_genomic.fna sequence.fasta
```

#### Extract FASTA Headers
```bash
grep "^>" sequence.fasta
```

#### Match Lines Ending with a Pattern
```bash
grep "5$" sequence.fasta
```

---

#### Installing a Text Editor

```bash
sudo apt-get install -y nano
```

---

#### Creating and Viewing a Log File

```bash
# Create an example log file
nano log_file.txt
```

```bash
# Display the contents
cat log_file.txt
```

---

#### Searching Patterns in Logs

```bash
# Match a 6-digit number
grep -E "[0-9]{6}" log_file.txt
```

```bash
# Search for the word "error"
grep "error" log_file.txt
```

```bash
# Case-insensitive search
grep -i "error" log_file.txt
```

---

#### Working with a Second Log File

```bash
# Create another example log file
nano log_file2.txt
```

```bash
# View the file
