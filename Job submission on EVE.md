# Job submission on EVE 
### EVE support
[WKDV Support](https://wkdv-support.ufz.de/#ticket/view/my_tickets)

maxvmem
wallclock. =)

### get statistics
qacct -j 6354975 | qacct-efficiency
qstat 
qstat -j <jobid> 
qacct -j <jobid>
watch qstat
watch qstat -u godinhop
qdel -f job_id
* * * *
# CheckM - script
```bash
#!/bin/bash
module load python/2
#$ -l h_rt=50:00:00
#$ -l h_vmem=9G
#$ -pe smp 5-24
#$ -o /gpfs1/data/msb/silva/fna2/logs2/$JOB_NAME-$JOB_ID.out
#$ -e /gpfs1/data/msb/silva/fna2/logs2/$JOB_NAME-$JOB_ID.err
source /gpfs1/data/msb/tools/checkm/checkm_env/bin/activate
#1 is the bin folder
#2 is the output folder
#3 is the output file
checkm lineage_wf -t ${NSLOTS:-1}  --tab_table -x fa -f $3 $1 $2
```
#### CheckM - submission of job 
##### done by Rodolfo: 
qsub -N sandra_bins_checkm /gpfs1/data/msb/tools/checkm/sub_script_ulisses.sh /data/msb/silva/fna/all_fna2/ /data/msb/silva/fna/checkm /data/msb/silva/fna/output_checkm.tsv

##### done by me:
qsub -N sandra_newbins_checkm /gpfs1/data/msb/tools/checkm/sub_script_ulisses.sh /data/msb/silva/fna/new_bin_folder2/ /data/msb/silva/fna2/checkm_newbins /data/msb/silva/fna/output_checkm_newbins.tsv

ImportError: /gpfs1/data/msb/tools/checkm/checkm_env/lib64/python2.7/lib-dynload/_io.so: undefined symbol: _PyCodec_LookupTextEncoding

# Mashtree 
```bash
#!/bin/bash
echo "First arg: $1"
echo "Second arg: $2"
#$ -l h_rt=24:00:00
#$ -l h_vmem=10G
#$ -pe smp 2-32
#$ -o /gpfs1/data/msb/tools/mashtree/logs/$JOB_NAME-$JOB_ID.out
#$ -e /gpfs1/data/msb/tools/mashtree/logs/$JOB_NAME-$JOB_ID.err
task="mashtree"
module load miniconda/2
source activate /data/msb/tools/mashtree/mashtree_conda
# input 1 is the folder containing the genomes
# input 2 is the dnd output tree
# please use full path for the inputs
echo "---> Starting with "$task
date
mashtree --numcpus  ${NSLOTS:-1} $1/* > $2
date
echo "---> Finished with"$task
```

### Submission
qsub -N sandra_bins_mashtree /gpfs1/data/msb/tools/mashtree/mashtree_subscript.sh /data/msb/silva/fna/new_bin_folder /data/msb/silva/fna/new_bin_folder/mashtree.dnd

# Mash 
```bash
#!/bin/bash
# loading modules
module load gsl
module load python/2
#$ -N mash__test
#$ -l h_rt=4:00:00
#$ -l h_vmem=1G
#$ -binding linear:1
# output files
###$ -o /gpfs1/data/msb/rodolfo/job_logs/$JOB_NAME-$JOB_ID.out
###$ -e /gpfs1/data/msb/rodolfo/job_logs/$JOB_NAME-$JOB_ID.err
#$ -o /gpfs1/data/msb/silva/fna/logs/$JOB_NAME-$JOB_ID.out
#$ -e /gpfs1/data/msb/silva/fna/logs/$JOB_NAME-$JOB_ID.err
echo -e "Reference-ID\tQuery-ID\tMash-distance\tP-value\tMatching-hashes"> $1/"mash_output.tsv"
# run mash distance for all
for a in $1/*fna; 
	do #echo $a; 
	for b in $1/*fna; 
		do #echo $b; 
		/gpfs1/data/msb/tools/Mash/mash dist $a $b >> $1/"mash_output.tsv"
	done ;
done
# once file is prepared, run clustering based on ANI using fastcluster
#source /data/msb/MuDoGeR/ADMIN/scripts/manag_scripts/brat_bin_merge/modules/bin/activate
#python /data/msb/MuDoGeR/ADMIN/scripts/manag_scripts/brat_bin_merge/mash_cluster.py $1/"mash_output.tsv" > $1/"tempo"
#mv $1/"tempo" $1/"ANI_subclusters.tsv"
# now bins can be used for reassembly, to generate a new bin
```
### Submission
qsub -N sandra_bins_ANI-table /gpfs1/data/msb/tools/Mash/mash_subscript.sh  /data/$

# GTDBtk - script
```bash
#!/bin/bash
#loading modules
module load python/2
module load hmmer
#load on environment
source /gpfs1/data/msb/tools/GTDB/gtdb-v0.3.3/bin/activate
#necessary path variable
export GTDBTK_DATA_PATH=/gpfs1/data/msb/tools/GTDB/external_data/release89
#resoruces
#$ -l h_rt=50:00:00
#$ -l h_vmem=60G  -pe smp 2-10
#output files
#$ -o /gpfs1/data/msb/silva/fna2/logs2/$JOB_NAME-$JOB_ID.out
#$ -e /gpfs1/data/msb/silva/fna2/logs2/$JOB_NAME-$JOB_ID.err
```
#### submission of job 
gtdbtk  classify_wf --extension  fa  --cpus $ {NSLOTS:-1} --genome_dir $1  --out_di$

qsub -N gtdbtk_tina  /data/msb/tools/GTDB/gtdb_ulisses.sh classify_wf --extension  fa  --cpus ${NSLOTS:-1} --genome_dir /data/msb/silva/  --out_dir /data/msb/silva/tinas_bins

qsub -N gtdbtk_tina  /data/msb/tools/GTDB/gtdb_ulisses.sh classify_wf --extension  fa  --cpus ${NSLOTS:-1} --genome_dir /data/msb/silva/sandra-83-mdt-bins  --out_dir /data/msb/silva/sandra-83-mdt-bins

* * * *
# Prokka
```bash
#!/bin/bash
# loading modules
module load gcc/4/8.1-3
#####$ -N $finalname
#$ -l h_rt=20:00:00
#$ -l h_vmem=20G -pe smp 2-32
# output files
#$ -o /data/msb/silva/job_logs/$JOB_NAME-$JOB_ID.out
#$ -e /data/msb/silva/job_logs/$JOB_NAME-$JOB_ID.err
source /data/msb/tools/miniconda/miniconda2/bin/activate
conda activate /data/msb/tools/metawrap/metawrap_env
unset LD_PRELOAD
date
metawrap annotate_bins -o $2 -b $1 
date
```

## submit prokka annotation on EVE:
qsub -N prokka_Week4 metawrap_annotate.sh /data/msb/silva/fna2/Weeksellaceae_bins/Week4 /data/msb/silva/Prokka_ano/Week4

with for loop:
From Rodolfo:

```bash
for i in input*; do qsub -N <job> <scriptp> <inputs> ; done
```
```bash
for i in *; do qsub -N $i  /data/msb/silva/metawrap_annotate.sh /data/msb/silva/fna2/Weeksellaceae_bins/$i /data/msb/silva/Prokka_ano/$i ; done
```
* * *
# OrthoFinder
```bash
###$ -binding linear:1
# loading modules
module load python/2
module load gcc
module load diamond
module load glib
source /gpfs1/data/msb/tools/orthofinder/env-orthofinder/bin/activate
#$ -S /bin/bash
#$ -l h_rt=72:00:00 
#$ -l h_vmem=80G 
#$ -pe smp 1-10
#$ -o /data/msb/silva/job_logs/$JOB_NAME-$JOB_ID.out
#$ -e /data/msb/silva/job_logs/$JOB_NAME-$JOB_ID.err
python /gpfs1/data/msb/tools/orthofinder/OrthoFinder-2.3.3_source/orthofinder/orthofinder.py -f $1 -S diamond -og -o $2
```

* * * *
# antismash 
```bash
#!/bin/bash
# loading modules
module load GCC/7.3.0-2.30  OpenMPI/3.1.1  GDAL/2.2.3-Python-3.6.6 Anaconda3/5.3.0
# load conda
conda activate /data/msb/tools/antismash/conda-antismash
#$ -l h_rt=5:00:00
#$ -l h_vmem=10G
#$ -binding linear:1 	# for single core	#
# output files
#$ -o /data/msb/silva/job_logs/antismash/$JOB_NAME-$JOB_ID.out
#$ -e /data/msb/silva/job_logs/antismash/$JOB_NAME-$JOB_ID.err
task="antismash"
date
echo "starting "$task
#1 is the input folder
#2 is the output folder
#3 is the 
antismash "$1" 
date
echo "finishing "$task
```

qsub -N trial4 /data/msb/silva/sub_scripts/submission_antismash.sh /data/msb/silva/antismash/*

qsub -N trial4 /data/msb/silva/sub_scripts/submission_antismash.sh /data/msb/silva/antismash/GCF_002023505.1_ASM202350v1_genomic.gbk

antismash EASRX806419_bacbin.4.fna --output-dir /data/msb/silva/antismash/Output3/ --genefinding-tool prodigal



--cf-borders-only
* * * *
## fastANI

module load anaconda
conda create --name fastani
conda update fastani
conda install -c bioconda fastani

for i in *.txt; do qsub /data/msb/silva/Liu/group_by_taxonomy.py /data/msb/silva/Liu/bins_organized/$i /data/msb/silva/Liu/bins_organized/$i /data/msb/silva/Liu/${i%.*} 3000 0 ; done
