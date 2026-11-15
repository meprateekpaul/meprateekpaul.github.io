# Practical 01: Understanding Linux Operating System and Essential Shell Commands for Bioinformatics

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S01 (Syllabus Practical P1)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO1 — Describe computational data architectures, manipulate high-throughput sequence files, and navigate biological operating systems.

---

## 1. Aim & Objectives

### Aim
To gain practical operational competency in the Linux operating system, understand hierarchical Unix filesystem architectures, master file manipulation utilities, and execute essential text-processing pipelines crucial for high-throughput biological sequence data.

### Objectives
1. Navigate the Linux hierarchical directory tree using absolute and relative path syntaxes (`pwd`, `cd`, `ls`).
2. Create, manipulate, copy, move, and remove files and directories (`mkdir`, `touch`, `cp`, `mv`, `rm`).
3. Inspect and view raw genomic sequence records using standard streaming viewers (`cat`, `less`, `head`, `tail`).
4. Execute command-line text stream processing and token counting on FASTA files (`wc -l`, `wc -c`, `wc -m`).
5. Filter sequence headers and extract motif lines using pattern-matching regular expressions with `grep`.
6. Construct multi-command streaming pipelines combining redirection operators (`>`, `>>`) and Unix pipes (`|`) to count and parse biological FASTA databases.

---

## 2. Background & Scientific Principle

Modern computational biology and high-throughput bioinformatics are anchored upon Unix-like operating systems (Linux and macOS Darwin). Unlike desktop graphical user interfaces (GUIs), the command-line interface (CLI) provides:
1. **Deterministic reproducibility:** Commands can be recorded, parameterized, audited, and embedded into automated shell pipelines.
2. **Scalability:** Gigabyte- and terabyte-scale next-generation sequencing (NGS) flat files (e.g., FASTQ, BAM, FASTA, VCF) cannot be opened in standard spreadsheet software without catastrophic memory exhaustion. CLI tools stream data line-by-line with minimal memory footprints.
3. **Remote high-performance computing (HPC):** Supercomputing clusters and cloud virtual machines run headless Linux instances navigated solely through SSH (Secure Shell).

### The Linux Filesystem Hierarchy
Linux organizes all storage volumes under a single unified root directory represented by a forward slash (`/`). Crucial standard directories include:
- `/` : Root directory, the parent of all subdirectories.
- `/home/<username>` or `/Users/<username>` : User home directory containing personal files, configuration files, and active workspaces.
- `/bin` & `/usr/bin` : Essential user binaries and core command executables (`ls`, `cat`, `grep`).
- `/tmp` : Ephemeral temporary file scratch space cleared upon reboot.

Path navigation requires distinguishing between:
- **Absolute Paths:** Complete paths starting strictly from the root `/` (e.g., `/home/student/CBBI/data/sequences/hbb_human_mrna.fasta`).
- **Relative Paths:** Paths resolved relative to the Current Working Directory (CWD). The dot `.` denotes the current directory, and the double dot `..` denotes the parent directory.

### Text Streaming, Standard Streams, and Pipelines
In the Unix computational model, every process opens three standard input/output channels:
1. `stdin` (Standard Input, file descriptor 0): Default stream reading from the keyboard.
2. `stdout` (Standard Output, file descriptor 1): Default stream writing normal output to the terminal screen.
3. `stderr` (Standard Error, file descriptor 2): Stream dedicated to error and diagnostic messages.

The Unix philosophy emphasizes small, single-purpose utilities that can be composed seamlessly:
- **Redirection Operator (`>`):** Diverts `stdout` to a file, overwriting existing file content.
- **Append Operator (`>>`):** Diverts `stdout` to a file, appending new data to the end of the file.
- **Pipe Operator (`|`):** Connects the `stdout` of the upstream command directly to the `stdin` of the downstream command in RAM without writing temporary intermediate files to disk.

For example, counting sequences in a multi-FASTA database:
```bash
grep -c "^>" globin_family_proteins.fasta
```
Here, `^>` instructs `grep` to match only lines whose first character is the FASTA definition symbol `>`, eliminating false matches if a sequence description contains `>` internally.

---

## 3. Required Software, Tools, and Input Datasets

### Environment & Software
- Operating System: Linux (Ubuntu 20.04/22.04 LTS, CentOS, or WSL2 on Windows) or macOS Terminal.
- Shell: Bash (`/bin/bash`) or Zsh (`/bin/zsh`).
- Core utilities: GNU Coreutils (`ls`, `pwd`, `mkdir`, `cp`, `mv`, `rm`, `cat`, `head`, `tail`, `wc`, `grep`, `less`).

### Input Datasets
All input sequence files are located in the local curriculum data directory:
- Relative path: `../../data/sequences/`
- Datasets used:
  1. `hbb_human_mrna.fasta` (Human hemoglobin subunit beta mRNA, `NM_000518.5`, 626 bp).
  2. `hbb_human_protein.fasta` (Human hemoglobin subunit beta protein, `NP_000509.1`, 147 aa).
  3. `globin_family_proteins.fasta` (Multi-FASTA file containing 7 human globin family paralogues: HBA1, HBB, HBD, HBG1, MB, NGB, CYGB).
  4. `hbb_vertebrate_orthologues.fasta` (Multi-FASTA containing HBB protein sequences from 9 vertebrate organisms).

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Directory Navigation and Workspace Setup
1. Launch the Linux terminal.
2. Identify your current working directory:
   ```bash
   pwd
   ```
3. Create an isolated lab working directory for Session 01 and enter it:
   ```bash
   mkdir -p ~/CBBI_Lab/S01_Linux
   cd ~/CBBI_Lab/S01_Linux
   pwd
   ```
4. Verify your current working path. Confirm that you are inside `S01_Linux`.

### Phase 2: Inspecting and Copying Course Datasets
1. List the files present in the course data sequences directory using relative navigation:
   ```bash
   ls -lh ../../../btech/Concepts_of_Bioinformatics/data/sequences/
   ```
   *(Note: Adjust the path if your repository root is located elsewhere, or inspect the absolute path `/Users/prateekpaul/Library/CloudStorage/GoogleDrive-prateekp@iiitd.ac.in/My Drive/IIITD/mygithub/btech/Concepts_of_Bioinformatics/data/sequences/`).*
2. Copy the globin multi-FASTA and human HBB sequences to your local folder:
   ```bash
   cp ../../../btech/Concepts_of_Bioinformatics/data/sequences/hbb_human_mrna.fasta .
   cp ../../../btech/Concepts_of_Bioinformatics/data/sequences/globin_family_proteins.fasta .
   cp ../../../btech/Concepts_of_Bioinformatics/data/sequences/hbb_vertebrate_orthologues.fasta .
   ```
3. List your directory contents in long format showing file sizes and permissions:
   ```bash
   ls -la
   ```

### Phase 3: Inspecting File Content (`cat`, `less`, `head`, `tail`)
1. Display the entire contents of the single mRNA record:
   ```bash
   cat hbb_human_mrna.fasta
   ```
2. Display the first 10 lines of the globin family multi-FASTA:
   ```bash
   head -n 10 globin_family_proteins.fasta
   ```
3. Display the last 15 lines of the vertebrate orthologues file:
   ```bash
   tail -n 15 hbb_vertebrate_orthologues.fasta
   ```
4. Interactively browse through the vertebrate orthologues multi-FASTA using `less`:
   ```bash
   less hbb_vertebrate_orthologues.fasta
   ```
   - Press `Spacebar` to advance one page.
   - Press `b` to go back one page.
   - Type `/Gorilla` and press `Enter` to search for Gorilla.
   - Press `n` to jump to next match.
   - Press `q` to exit `less`.

### Phase 4: Token Counting (`wc`)
1. Determine the number of lines, words, and byte/character counts for `hbb_human_mrna.fasta`:
   ```bash
   wc hbb_human_mrna.fasta
   ```
2. Specifically count only the total number of lines in `globin_family_proteins.fasta`:
   ```bash
   wc -l globin_family_proteins.fasta
   ```

### Phase 5: Pattern Matching with `grep`
1. Search and print all header definition lines in `globin_family_proteins.fasta`:
   ```bash
   grep "^>" globin_family_proteins.fasta
   ```
2. Count the exact number of sequence records contained in `globin_family_proteins.fasta`:
   ```bash
   grep -c "^>" globin_family_proteins.fasta
   ```
3. Search for records mentioning "Homo sapiens" in `hbb_vertebrate_orthologues.fasta`:
   ```bash
   grep "Homo sapiens" hbb_vertebrate_orthologues.fasta
   ```
4. Display header lines alongside their line numbers:
   ```bash
   grep -n "^>" globin_family_proteins.fasta
   ```
5. Invert the match to print sequence lines only (excluding headers):
   ```bash
   grep -v "^>" hbb_human_mrna.fasta | head -n 5
   ```

### Phase 6: Pipes, Redirection, and Custom Filtering
1. Extract all header lines from `hbb_vertebrate_orthologues.fasta` and redirect them into a new file named `vertebrate_headers.txt`:
   ```bash
   grep "^>" hbb_vertebrate_orthologues.fasta > vertebrate_headers.txt
   ```
2. Append the globin family headers to the same file:
   ```bash
   grep "^>" globin_family_proteins.fasta >> vertebrate_headers.txt
   ```
3. Verify the combined file line count:
   ```bash
   wc -l vertebrate_headers.txt
   ```
4. Count the number of amino acid residues in `hbb_human_protein.fasta` (excluding header and newlines):
   ```bash
   grep -v "^>" ../../../btech/Concepts_of_Bioinformatics/data/sequences/hbb_human_protein.fasta | tr -d '\n' | wc -m
   ```

---

## 5. Offline Fallback Note

If local paths cannot be accessed or cloned, direct fallback sequence files are located in:
- `btech/Concepts_of_Bioinformatics/data/sequences/`
All standard Unix shell commands demonstrated in this lab run 100% locally on any Unix terminal without requiring active internet connectivity or external web server connections.

---

## 6. Observations Table

Record your terminal outputs in the following structured observation tables.

### Table 1.1: File Navigation and Basic Metrics
| Command Executed | Target File | Output / Value Observed | Biological / Operational Meaning |
|---|---|---|---|
| `pwd` | N/A | | |
| `ls -lh hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | | |
| `wc -l hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | | |
| `wc -c hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | | |
| `grep -c "^>" globin_family_proteins.fasta` | `globin_family_proteins.fasta` | | |
| `grep -c "^>" hbb_vertebrate_orthologues.fasta` | `hbb_vertebrate_orthologues.fasta` | | |

### Table 1.2: Header Identification from Multi-FASTA Files
| File | Total Records Found | Extracted Header Lines (First 3) |
|---|---|---|
| `globin_family_proteins.fasta` | | 1. <br>2. <br>3. |
| `hbb_vertebrate_orthologues.fasta` | | 1. <br>2. <br>3. |

---

## 7. Interpretation & Discussion Questions

1. **Header Identification Syntax:** Why is it computationally essential to search for `"^>"` rather than simply `">"` when counting or parsing FASTA files with `grep`? What error could occur if a sequence annotation line or quality score contains a `>` character?
2. **Line Count vs. Sequence Length:** Why does running `wc -l hbb_human_mrna.fasta` give 11 lines, whereas the actual mRNA transcript length is 626 nucleotides? Explain the difference between physical newline characters in text formatting and biological sequence coordinates.
3. **Pipes vs. Intermediate Files:** Contrast using a Unix pipe (`grep -v "^>" file.fasta | tr -d '\n' | wc -m`) versus creating temporary intermediate text files on disk. Why is piping superior for processing gigabyte-sized whole-genome FASTQ datasets?
4. **Redirection Safeguards:** What is the critical operational danger of confusing `>` with `>>` when logging analytical output from a long-running computational experiment?
5. **Character Counting:** Why does running `wc -m` directly on `hbb_human_mrna.fasta` report 637 characters when the official NCBI RefSeq record length is exactly 626 nucleotides? What do the extra 11 characters represent?

---

## 8. Extension / Challenge Task (For Advanced Students)

Write a single one-line Bash shell command pipeline that:
1. Takes the multi-FASTA file `globin_family_proteins.fasta`.
2. Computes the sequence length (number of amino acids, excluding headers and newlines) for **each individual protein** in the file.
3. Outputs the sequence header followed by its calculated length in a neat two-column tabular format:
   ```
   >NP_000508.1 hemoglobin subunit alpha 142
   >NP_000509.1 hemoglobin subunit beta 147
   ...
   ```
*(Hint: Use `awk` or a combination of `while read` loop in bash).*
