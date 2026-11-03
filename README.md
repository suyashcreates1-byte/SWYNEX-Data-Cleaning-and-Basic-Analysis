# SWYNEX-Data-Cleaning-and-Basic-Analysis# Task 2: Data Cleaning and Basic Analysis

## Dataset Overview
**Dataset:** SARS-CoV-2 Reference Genome (Accession: NC_045512)
**Source:** National Center for Biotechnology Information (NCBI)

## Project Objective
The goal of this task is to clean raw genomic FASTA data by removing metadata and non-sequence characters, and to perform a basic analysis by calculating the total genome length and the GC-content.

## Python Script
Below is the Python code used to read, clean, and analyze the dataset. To ensure accurate counting, the script isolates the genetic sequence by splitting the raw text at the word "ORIGIN", ignoring the English metadata at the top of the file.

```python
# Open and read the raw FASTA file
with open('sars-cov-2-genome.fasta', 'r') as file:
    raw_data = file.read()

# Split the document at the word "ORIGIN" to remove metadata
if "ORIGIN" in raw_data:
    genome_data = raw_data.split("ORIGIN")[1]
else:
    genome_data = raw_data

# Clean the data by extracting only alphabetical characters
clean_sequence = "" 
for char in genome_data:
    if char.isalpha(): 
        clean_sequence += char.upper()

# Analyze the data
total_length = len(clean_sequence)
count_A = clean_sequence.count('A')
count_T = clean_sequence.count('T')
count_C = clean_sequence.count('C')
count_G = clean_sequence.count('G')

gc_content = ((count_G + count_C) / total_length) * 100

# Print results
print("--- CORRECTED Data Cleaning Results ---")
print(f"Total Genome Length: {total_length} base pairs")
print(f"Adenine (A): {count_A}")
print(f"Thymine (T): {count_T}") 
print(f"Cytosine (C): {count_C}")
print(f"Guanine (G): {count_G}")
print(f"GC-Content: {round(gc_content, 2)}%")
