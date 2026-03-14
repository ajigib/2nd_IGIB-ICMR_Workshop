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


#### Installing a Text Editor

```bash
sudo apt-get install -y nano
```


#### Creating and Viewing a Log File

```bash
# Create an example log file
nano log_file.txt
```

```bash
# Display the contents
cat log_file.txt
```


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


#### Working with a Second Log File

```bash
# Create another example log file
nano log_file2.txt
```
---

### awk

`awk` is a powerful programming language and command-line utility used for **pattern scanning and text processing**.  
It processes input data **line by line (records)** and splits each line into **columns (fields)**, usually separated by spaces or tabs.  

It is widely used for:
- Column-based data manipulation
- Filtering rows based on conditions
- Extracting fields from structured files
- Bioinformatics data processing (FASTA, GTF, BED, FASTQ)


#### Viewing File Contents

Display the contents of a file.

```bash
cat expression.tsv
```

#### Extract Specific Columns

Print the **1st and 3rd columns** from a tabular file.

```bash
awk '{print $1, $3}' expression.tsv
```

Explanation:
- `$1` → first column  
- `$3` → third column  
- `print` → outputs selected fields  
- Default separator is a space.


#### Print Columns with Tab Separation

Print the **1st and 3rd columns separated by a tab**.

```bash
awk '{print $1 "\t" $3}' expression.tsv
```

Explanation:
- `"\t"` inserts a **tab character** between fields.


#### Filter Rows Based on a Condition

Print rows where the **value in column 5 is greater than 1**.

```bash
awk '$5 > 1' expression.tsv
```

Explanation:
- `$5` → fifth column
- `> 1` → condition applied to filter rows
- Only rows satisfying the condition are printed.


#### Display a GTF Annotation File

```bash
cat annotations.gtf
```

This prints the entire **GTF annotation file**, commonly used for gene annotations.


#### Extract Gene Coordinates

Print chromosome, start, end, and strand for **gene entries**.

```bash
awk '$3=="gene" {print $1, $4, $5, $7}' annotations.gtf
```

Explanation:
- `$3=="gene"` → selects rows describing genes
- `$1` → chromosome
- `$4` → start coordinate
- `$5` → end coordinate
- `$7` → strand (+ or -)


#### Filter Only Exon Features

```bash
awk '$3=="exon"' annotations.gtf
```

Explanation:
- Filters rows where the **third column equals "exon"**.


#### Filter Rows by Chromosome

```bash
awk '$1 == "chr1"' regions.bed
```

Explanation:
- `$1` → chromosome column
- Prints rows that belong to **chromosome 1**.


#### Calculate Interval Length

Add a new column representing the **length of genomic intervals**.

```bash
awk '{print $0 "\t" $3 - $2}' regions.bed
```

Explanation:
- `$0` → entire line
- `$3 - $2` → interval length (end − start)
- `"\t"` adds the new value as another column.

#### Extract Sequence Lines from FASTQ

```bash
awk 'NR%4==2' reads.fastq
```

Explanation:
- `NR` → current line number
- `NR % 4 == 2` → selects **every 2nd line in a 4-line FASTQ record**
- FASTQ format structure:

```
Line 1: @sequence_id
Line 2: DNA sequence
Line 3: +
Line 4: quality scores
```

This command extracts **only the DNA sequence lines**.

---
### sed — Stream Editor

`sed` (Stream Editor) is a command-line utility used to **perform text transformations on streams of text or files**.  
It is commonly used for:

- Find and replace operations
- Deleting lines
- Extracting sections of files
- Formatting text
- Simple automated editing of files

It processes input **line by line** and applies editing commands.

#### Remove Prefix at Beginning of Line

Remove `"chr"` only if it appears at the **start of a line**.

```bash
sed 's/^chr//' regions.bed
```

Explanation:
- `s` → substitute command  
- `^chr` → matches `"chr"` only at the **beginning of a line**  
- Replaces it with nothing (effectively deleting it).


#### View File Contents

```bash
cat annotations.gtf
```

Displays the contents of the **GTF annotation file**.


#### Find and Replace Text

Replace `"chr"` with `"scaffold_"` in the file output.

```bash
sed 's/chr/scaffold_/g' annotations.gtf
```

Explanation:
- `s` → substitute
- `chr` → search pattern
- `scaffold_` → replacement
- `g` → replace **all matches in each line**.

#### Replace Text In-Place

Modify the file directly instead of printing to the terminal.

```bash
sed -i 's/chr/scaffold_/g' annotations.gtf
```

Explanation:
- `-i` → edit the file **in place**.

#### Revert Replacement

Replace `"scaffold_"` back to `"chr"`.

```bash
sed -i 's/scaffold_/chr/g' annotations.gtf
```

#### View Updated File

```bash
cat annotations.gtf
```

Displays the modified file.

#### View FASTA File

```bash
cat sequence2.fasta
```

Shows the FASTA sequence file.

#### Remove FASTA Headers

Delete lines starting with `>` (FASTA header lines).

```bash
sed '/^>/d' sequence2.fasta
```

Explanation:
- `/^>/` → matches lines beginning with `>`
- `d` → deletes those lines.


#### View VCF File

```bash
cat variants.vcf
```

Displays the variant file.

#### Remove Comment Lines from VCF

```bash
sed '/^#/d' variants.vcf
```

Explanation:
- `/^#/` → matches lines beginning with `#`
- `d` → deletes comment lines.

#### Extract Lines Between Two Markers

Extract a specific FASTA entry.

```bash
sed -n '/^>gene123/,/^>/p' sequence2.fasta
```

Explanation:
- `-n` → suppress automatic printing
- `/^>gene123/` → start at header `gene123`
- `/^>/` → stop at next FASTA header
- `p` → print the selected region.

#### Replace Tabs with Spaces

```bash
sed 's/\t/ /g' file.gff
```

Explanation:
- `\t` → tab character
- Replaces each tab with a space.

#### Collapse Multiple Spaces

```bash
sed 's/  */ /g' multispace_file.txt
```

Explanation:
- `  *` → matches two or more spaces
- Replaces them with a **single space**.


#### Convert FASTA Sequences to Lowercase

```bash
sed '/^>/! s/.*/\L&/' sequence2.fasta
```

Explanation:
- `/^>/!` → apply command to **non-header lines only**
- `\L` → convert text to lowercase
- `&` → entire matched line.


#### Convert FASTA Sequences to Uppercase

```bash
sed '/^>/! s/.*/\U&/' sequence2.fasta
```

Explanation:
- `\U` → converts text to uppercase
- Headers remain unchanged.

#### Create Backup While Editing

```bash
sed -i.bak 's/sample3/sample4/g' expression.tsv
```

Explanation:
- `-i.bak` → edit file and **create a backup** with `.bak` extension.


#### View Backup File

```bash
cat expression.tsv.bak
```

Displays the backup copy.

#### Delete the First N Lines

Delete the first **4 lines** of the file.

```bash
sed '1,4d' expression.tsv
```

Explanation:
- `1,4` → line range
- `d` → delete those lines.
