#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`

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



###Attributes of `snp_position.txt`

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



##Data Processing

###Maize Data

```
$ grep -E "(Sample_ID|ZMMIL|ZMMLR|ZMMMR)" fang_et_al_genotypes.txt > maize.txt
$ awk -f transpose.awk maize.txt > transposed_maize_genotypes.txt 
$ sort -k1,1n transposed_maize_genotype.txt > sorted_transposed_maize_genotype.txt
$ sort -k1,1n snp_position.txt > sorted_snp_position.txt   
$ join -1 1 -2 1 -t $'\t' -a 1 sorted_snp_position.txt sorted_transposed_maize_genotypes.txt >    complete_maize.txt
$ awk '$3 ~ /^1$/' complete_maize.txt | sort -k4,4n > chr1_maize_increasing.txt #ran this line of code for all 10 chromosomes for sorting by increasing position
$ awk '$3 ~ /^1$/' complete_maize.txt | sort -k4,4nr | sed 's/?/-/g' > chr1_maize_decreasing.txt
  #ran this line of code for all 10 chromosomes for sorting by decreasing position
$ grep "unknown" complete_maize.txt > SNP_unknown_positions.txt
$ grep "multiple" complete_maize.txt > SNP_multiple_positions
$ mkdir ChrDecreasing
$ mv chr*_maize_decreasing ChrDecreasing/
$ mkdir ChrIncreasing
$ mv chr*_maize_increasing ChrIncreasing/


```

Here is my brief description of what this code does


###Teosinte Data

```
$ grep -E "(Sample_ID|ZMPBA|ZMPIL|ZMPJA)" fang_et_al_genotypes.txt > teosinte.txt
$ awk -f transpose.awk teosinte.txt > transposed_teosinte_genotypes.txt
$ sort -k1,1n transposed_teosinte_genotypes.txt > sorted_transposed_teosinte_genotypes.txt
$ sort -k1,1n snp_position.txt > sorted_snp_position.txt   
$ join -1 1 -2 1 -t $'\t' -a 1 sorted_snp_position.txt sorted_transposed_teosinte_genotypes.txt > complete_teosinte.txt
$ awk '$3 ~ /^1$/' complete_teosinte.txt | sort -k4,4n > chr1_teosinte_increasing.txt #ran this line of code for all 10 chromosomes for sorting by increasing position
$ mkdir teosinte_chr_increasing
$ mv chr*_teosinte_increasing.txt teosinte_chr_increasing/
$ awk '$3 ~ /^1$/' complete_teosinte.txt | sort -k4,4nr | sed 's/?/-/g' > chr1_teosinte_decreasing.txt # ran this line of code for all 10 chromosomes for sorting by decreasing positions
$ mkdir teosinte_chr_decreasing
$ mv chr*_teosinte_decreasing.txt teosinte_chr_decreasing/






```

Here is my brief description of what this code does
