# UNIX Assignment

## Data Inspection

### Attributes of `fang_et_al_genotypes`

```
$ wc fang_et_al_genotypes.txt
$ du -h fang_et_al_genotypes.txt
$ awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt
$ tail -n +6 fang_et_al_genotypes.txt | awk -F "\t" '{print NF; exit}'
```

By inspecting this file I learned that:

1. There are 2783 lines, 2744038 words, and 11051939 bytes. 
2. The file size of this document in 6.1 MB. 
3. There are 986 columns in this file.



### Attributes of `snp_position.txt`

```
$ wc snp_position.txt
$ du -h snp_position.txt
$ awk -F "\t" '{print NF; exit}' snp_position.txt
$ tail -n +6 snp_position.txt | awk -F "\t" '{print NF; exit}'
```

By inspecting this file I learned that:

1. There are 984 lines, 13198 words, and 82763 bytes.
2. The file size of this document is 38KB.
3. There are 15 columns in this file. 



## Data Processing

### Maize Data

```
$ cut -f1,3,4 snp_position.txt > cut_snp_position.txt
$ grep -E "(Sample_ID|ZMMIL|ZMMLR|ZMMMR)" fang_et_al_genotypes.txt > maize.txt
$ awk -f transpose.awk maize.txt > transposed_maize_genotypes.txt 
$ sort -k1,1 transposed_maize_genotypes.txt > sorted_transposed_maize_genotypes.txt
$ sort -k1,1 cut_snp_position.txt > sorted_cut_snp_position.txt   
$ join -1 1 -2 1 -t $'\t' -a 1 sorted_cut_snp_position.txt sorted_transposed_maize_genotypes.txt > complete_maize.txt
$ awk '$2 ~ /^1$/' complete_maize.txt | sort -k3,3n > chr1_maize_increasing.txt #ran this line of code for all 10 chromosomes for sorting by increasing position
$ awk '$2 ~ /^1$/' complete_maize.txt | sort -k3,3nr | sed 's/?/-/g' > chr1_maize_decreasing.txt
  #ran this line of code for all 10 chromosomes for sorting by decreasing position
$ awk '$3 ~ /^unknown$/' complete_maize.txt > SNP_unknown_positions.txt
$ awk '$3 ~ /^multiple$/' complete_maize.txt > SNP_multiple_positions.txt
$ mkdir maize_chr_decreasing
$ mv chr*_maize_decreasing ChrDecreasing/
$ mkdir maize_chr_increasing
$ mv chr*_maize_increasing ChrIncreasing/
```

In the code above, I first cut the columns necessary from the snp_position.txt (columns 1, 3, and 4). I then separated the maize data from the fang_et_al_genotypes.txt using the "grep" command. After transposing this document, I sorted the data by the 1st column (Sample_ID). I then sorted the cut_snp_position.txt document by the first column (SNP_ID) and joined this document with the transposed_maize_genotype.txt document by the common column (column 1). I then separated data from the first chromosome using the awk command, followed by a pipe to sort by increasing position. I ran this line of code 10 times for all of the chromosomes. Missing data is already represented by a "?". I repeated the same code for all chromosomes for decreasing position (adding "r" in the sort command), followed by a pipe to change "?" to "-" using the sed command. I then separated SNPs with "unknown" and "multiple" positions using the awk command. I created folders for the increasing and decreasing chromosome documents and moved the correct documents into each. 



### Teosinte Data

```
$ grep -E "(Sample_ID|ZMPBA|ZMPIL|ZMPJA)" fang_et_al_genotypes.txt > teosinte.txt
$ awk -f transpose.awk teosinte.txt > transposed_teosinte_genotypes.txt
$ sort -k1,1 transposed_teosinte_genotypes.txt > sorted_transposed_teosinte_genotypes.txt
$ sort -k1,1 cut_snp_position.txt > sorted_cut__snp_position.txt   
$ join -1 1 -2 1 -t $'\t' -a 1 sorted_cut_snp_position.txt sorted_transposed_teosinte_genotypes.txt > complete_teosinte.txt
$ awk '$2 ~ /^1$/' complete_teosinte.txt | sort -k3,3n > chr1_teosinte_increasing.txt #ran this line of code for all 10 chromosomes for sorting by increasing position
$ mkdir teosinte_chr_increasing
$ mv chr*_teosinte_increasing.txt teosinte_chr_increasing/
$ awk '$2 ~ /^1$/' complete_teosinte.txt | sort -k3,3nr | sed 's/?/-/g' > chr1_teosinte_decreasing.txt # ran this line of code for all 10 chromosomes for sorting by decreasing positions
$ mkdir teosinte_chr_decreasing
$ mv chr*_teosinte_decreasing.txt teosinte_chr_decreasing/
$ awk '$3 ~ /^multiple$/' complete_teosinte.txt > SNP_teosinte_multiple_positions.txt
$ awk '$3 ~ /^unknown$/' complete_teosinte.txt > SNP_teosinte_unknown_positions.txt
```

In the code above, I separate the teosinte data from the fang_et_al_genotypes.txt using the "grep" command. After transposing this document, I sorted the data by the 1st column (Sample_ID). I then sorted the cut_snp_position.txt document by the first column and joined this document with the transposed_teosinte_genotype.txt document by the common column (column 1). I then separated data from the first chromosome using the awk command, followed by a pipe to sort by increasing position. I ran this line of code 10 times for all chromosomes. Missing data is already represented by a "?". I repeated the same code for all chromosomes for decreasing position (adding "r" in the sort command), followed by a pipe to change "?" to "-" using the sed command. I then separated SNPs with "unknown" and "multiple" positions using the awk command. I created folders for the increasing and decreasing chromosome documents and moved the correct documents into each. 
