# Miscelaneous utilities

## activate conda - desktop
```bash
source /home/gomes/anaconda3/bin/activate
conda activate silva-env
```

## Permissions
```bash
setfacl -R -m d:u:USERX:rwX /path/to/folder
```

## others
for bin in folder/* ; do  grep "$( echo $bin | sed "s/new_bin_folder\///g"  | sed "s/.fna//g")" taxonomy.tsv ; done > new_taxonomy.tsv




