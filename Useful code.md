# Useful code
### create conda environment on eve
```bash
conda create -p /data/msb/sandra/conda_env_for_bla
```
### Clear screen
```bash
clear
```
### Copy all files with extension x to folder x
```bash
find . -name \*.gbk -exec cp {} /data/msb/silva/Prokka_ano/prokka_out/Gbk/ \;
```
### Remove empty folders in the directory
first:
```bash
find . -type d -empty -print
```
final:
```bash
find . -type d -empty -delete
```
* * * *
## Move files
### Move files into subdirectories
**folder_divider.sh**
```bash
#!/bin/sh
d=1                # index of the directory
f=0                # number of files already copied into direc$d
for x in *; do     # iterate over the files in the current directory
  #Create the target directory if this is the first file to be copied there
  if [ $f -eq 0 ]; then mkdir "direc$d"; fi
  #Move the file
  mv -- "$x" "direc$d"
  f=$((f+1))
  #If we've moved 5 files, go on to the next directory
  if [ $f -eq 5 ]; then
    f=0 d=$((d+1))
  fi
done
```
### Move 100 files into subdirectory
ls -rt source/* | head -n100 | xargs cp -t destination

### Move all files from subdirectories to current directory
```bash
find ./*/* -type f -print0 | xargs -0 -I % mv % .
```
### Move files into n folders
```bash
i=0; for f in *; do d=dir_$(printf %03d $((i/100+1))); mkdir -p $d; echo "$f" $d; let i++; done
```
substitute echo per mv to be able to test first
change 100 for the desired number of files per folder
### Group files from subfolders in same folder by pattern:
```bash
find . -name 'tax*' -exec mv "{}" ~/silva/Liu_et.al_2020/bins_organized4/Tax/ \;
```
* * * *
## Others

### Rename
```bash
rename .fna .fa *.fna
```
**confirm:**
```bash
head *filename*
```
### Remove spaces in headers of fna files:
```bash
sed 's, ,_,g' -i *.fna
```
### remove last part of filename:

{i%.*}
* * * *
## Lists
### getting unique IDs into List
```bash
ls *fna | cut -f2 -d'_' | sort | uniq -c | column -t | awk -F' ' '{ if ($1==1) {print } }' | cut -f3 -d' ' > LIST_UNIQUE
```
### getting duplicated IDs into List
```bash
ls *fna | cut -f2 -d'_' | sort | uniq -c | column -t | awk -F' ' '{ if ($1==2) {print } }'| cut -f3 -d' ' > LIST_DUPLICATES
```
### copying to new folder the files that are in list
```bash
while read l; do  cp  all_fna2/GCF_"$l"* new_bin_folder/ ; done < LIST_DUPLICATES 
```
### iterate through list
```bash 
while read l; do  cp  all_fna2/*"$l"* new_bin_folder/ ; done < LIST_UNIQUE
```

### create folders that are in list
```bash 
while read l; do mkdir /data/msb/silva/COG/Output_cogs/${l%.*}; done < LIST.txt
```
### copy from list with partial matching
```bash 
while read l; do cp  $l* /data/msb/silva/missing_genomes/ ; done < /data/msb/silva/LIST_missing.csv
```
### correct indentation in file:
```bash
perl -i.bak -pe "s/\t/' 'x(4-pos()%4)/eg" file.py
```
### change file name as in list:
```bash
while read l ; do mv ${l%.*}_out $l; done < /data/msb/silva/NEW/assembly_ids.tsv
```