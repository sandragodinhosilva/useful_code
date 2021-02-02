# Utilities
```bash
ssh godinhop@frontend2.eve.ufz.de
```
```bash
ssh darocha@frontend2.eve.ufz.de
```
Mariana2020!!

ssh://godinhop@frontend2.eve.ufz.de/data/msb/silva

ssh://darocha@frontend2.eve.ufz.de/data/msb/silva


sandra.silva@ufz.de
Laranja_1414_
VPN certificate: 31693169

## scp example
scp /home/gomes/Script/contig_namer.py darocha@frontend2.eve.ufz.de:/data/msb/silva/fna2

/data/msb/joao/tinas_bins

## run python3 script on Ulisses's eve:
```bash
module purge
module load python/3.3.0-1-virtual
python script.py 
```


## activate conda - desktop
```bash
source /home/gomes/anaconda3/bin/activate
conda activate silva-env
```

## Permissions
```bash
setfacl -R -m u:darocha:rwX -m d:u:darocha:rwX /data/msb/silva

setfacl -R -m u:godinhop:rwX -m d:u:godinhop:rwX /data/msb/silva/fna2/sandra-83-mdt-bins
```

## others
for bin in new_bin_folder/* ; do  grep "$( echo $bin | sed "s/new_bin_folder\///g"  | sed "s/.fna//g")" taxonomy.tsv ; done > new_taxonomy.tsv

darocha@frontend2 /data/msb/silva/fna/checkm/bins $ for bin in new_bin_folder/* ; do  grep "$( echo $bin | sed "s/new_bin_folder\///g"  | sed "s/.fna//g")" taxonomy.tsv ; done > new_taxonomy.tsv




