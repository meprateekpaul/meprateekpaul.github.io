# Instructor Answer Key & Evaluation Manual: Practical 01 (Linux Commands)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S01 (Syllabus Practical P1)  
**Curriculum Topic:** Understanding Linux Operating System and Commands  

---

## 1. Expected Outputs & Reference Solutions

### Table 1.1: File Navigation and Basic Metrics (Completed)
| Command Executed | Target File | Output / Value Observed | Biological / Operational Meaning |
|---|---|---|---|
| `pwd` | N/A | `/home/student/CBBI_Lab/S01_Linux` (or active user path) | Current absolute working path |
| `ls -lh hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | `-rw-r--r-- ... 699B ... hbb_human_mrna.fasta` | File size is 699 bytes; read/write owner, read group/others |
| `wc -l hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | `11 hbb_human_mrna.fasta` | 1 header line + 10 sequence lines = 11 lines |
| `wc -c hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | `699 hbb_human_mrna.fasta` | Total 699 bytes (including ASCII header and newline characters) |
| `grep -c "^>" globin_family_proteins.fasta` | `globin_family_proteins.fasta` | `7` | Exactly 7 human globin family protein paralogues |
| `grep -c "^>" hbb_vertebrate_orthologues.fasta` | `hbb_vertebrate_orthologues.fasta` | `9` | Exactly 9 vertebrate HBB protein orthologues |

### Table 1.2: Header Identification from Multi-FASTA Files (Completed)
| File | Total Records Found | Extracted Header Lines (First 3 Records) |
|---|---|---|
| `globin_family_proteins.fasta` | `7` | 1. `>NP_000508.1 hemoglobin subunit alpha [Homo sapiens]`<br>2. `>NP_000509.1 hemoglobin subunit beta [Homo sapiens]`<br>3. `>NP_000510.1 hemoglobin subunit delta [Homo sapiens]` |
| `hbb_vertebrate_orthologues.fasta` | `9` | 1. `>NP_000509.1 hemoglobin subunit beta [Homo sapiens]`<br>2. `>XP_001168847.1 hemoglobin subunit beta [Pan troglodytes]`<br>3. `>XP_004044558.1 hemoglobin subunit beta [Gorilla gorilla gorilla]` |

---

## 2. Sample Terminal Transcript

```bash
$ cd ~/CBBI_Lab/S01_Linux
$ grep -c "^>" globin_family_proteins.fasta
7
$ grep -c "^>" hbb_vertebrate_orthologues.fasta
9
$ grep "^>" globin_family_proteins.fasta
>NP_000508.1 hemoglobin subunit alpha [Homo sapiens]
>NP_000509.1 hemoglobin subunit beta [Homo sapiens]
>NP_000510.1 hemoglobin subunit delta [Homo sapiens]
>NP_000550.2 hemoglobin subunit gamma-1 [Homo sapiens]
>NP_005359.1 myoglobin [Homo sapiens]
>NP_067080.1 neuroglobin [Homo sapiens]
>NP_599030.1 cytoglobin [Homo sapiens]
$ grep -v "^>" hbb_human_protein.fasta | tr -d '\n' | wc -m
147
```

---

## 3. Model Answers to Discussion Questions

### Q1. Header Identification Syntax (`^>` vs `>`)
- **Model Answer:** The carat symbol `^` is a regular expression anchor that restricts the search to occurrences at the **start of the line**. In FASTA format, sequence identifier definition lines begin with `>` in column 1. However, description lines may include mathematical relational operators (e.g., `>90% identity`), or experimental annotations containing `>`. If `grep -c ">"` is run, any line containing an internal `>` would trigger a false-positive sequence count. Anchoring with `"^>"` guarantees that only true FASTA headers are matched.

### Q2. Line Count vs. Sequence Length
- **Model Answer:** Standard FASTA flat files adhere to line-wrapping standards (historically 60, 70, or 80 characters per line) to maintain legibility in terminals and printed documents. In `hbb_human_mrna.fasta`, the 626 nucleotide transcript is wrapped across 10 sequence lines (each ending with a line-feed character `\n`), plus 1 header line, yielding a total of 11 lines. `wc -l` counts newline characters (`\n`), not biological nucleotides. Biological length corresponds to the sum of sequence characters, excluding formatting newlines and header text.

### Q3. Pipes vs. Intermediate Files
- **Model Answer:** Pipes (`|`) stream the output of an upstream process directly through shared memory (RAM buffers) into the standard input of the downstream process without writing ephemeral files to physical storage disks. For massive high-throughput sequencing datasets (e.g., 50 GB FASTQ files), writing intermediate uncompressed text files incurs massive I/O disk bottlenecks, consumes storage quotas, and risks filesystem fragmentation. Streaming Unix pipelines minimize latency and disk writes.

### Q4. Redirection Safeguards (`>` vs `>>`)
- **Model Answer:** The single right-angle bracket `>` is a destructive redirection operator that immediately truncates/overwrites the target destination file if it already exists. In contrast, double brackets `>>` append new data to the bottom of the existing file. Accidentally using `>` instead of `>>` in an iterative loop or multi-step logging script completely wipes all historical data gathered in previous steps.

### Q5. Character Counting in `hbb_human_mrna.fasta`
- **Model Answer:** Running `wc -c` or `wc -m` directly on the file counts every single byte/character in the physical file. The file `hbb_human_mrna.fasta` contains:
  - 1 header line: `>NM_000518.5 Homo sapiens hemoglobin subunit beta (HBB), mRNA` (62 characters) + 1 newline (`\n`) = 63 bytes.
  - 10 wrapped sequence lines containing 626 nucleotide characters + 10 newline characters (`\n`) = 636 bytes.
  - Total byte size = 63 + 636 = 699 bytes.
  The extra 73 characters represent the FASTA header, sequence metadata, and newline delimiters.

---

## 4. Solution to Extension / Challenge Task

### Method 1: Using `awk` (Standard Industry Idiom)
```bash
awk '/^>/ {if (seq) print header, length(seq); header=$0; seq=""; next} {seq=seq $0} END {if (seq) print header, length(seq)}' globin_family_proteins.fasta
```

### Method 2: Pure Shell While-Loop
```bash
while read -r line; do
  if [[ "$line" =~ ^\> ]]; then
    if [[ -n "$header" ]]; then
      echo "$header $count"
    fi
    header="$line"
    count=0
  else
    len=$(echo -n "$line" | wc -m)
    count=$((count + len))
  fi
done < globin_family_proteins.fasta
echo "$header $count"
```

### Expected Output
```
>NP_000508.1 hemoglobin subunit alpha [Homo sapiens] 142
>NP_000509.1 hemoglobin subunit beta [Homo sapiens] 147
>NP_000510.1 hemoglobin subunit delta [Homo sapiens] 147
>NP_000550.2 hemoglobin subunit gamma-1 [Homo sapiens] 147
>NP_005359.1 myoglobin [Homo sapiens] 154
>NP_067080.1 neuroglobin [Homo sapiens] 151
>NP_599030.1 cytoglobin [Homo sapiens] 190
```

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab understanding** | 2.0 | Deduct 0.5 for incorrect explanation of absolute vs relative paths. |
| **Command Execution & Pipes** | 4.0 | Deduct 1.0 if pipes are not used correctly or `wc` is confused with nucleotide length. Deduct 1.0 if student fails to run `grep -c "^>"`. |
| **Observation Tables** | 2.0 | Deduct 0.5 per missing or incorrect metric in Table 1.1 or 1.2. |
| **Discussion & Analysis** | 2.0 | Award 0.4 marks per question for scientifically rigorous explanation. |
| **Total** | **10.0** | |
