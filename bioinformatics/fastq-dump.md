Source: https://edwards.sdsu.edu/research/fastq-dump/

We usually use this command (changing SRR_ID to whatever the ID is).
```
fastq-dump --outdir fastq --gzip --skip-technical  --readids --read-filter pass --dumpbase --split-3 --clip SRR_ID
```


After that, and depending on your downstream analyses, you may need to reorganize the fastq files so that the sequences in each file match and that you get file(s) of singletons. 
I suggest that you try fastq_pair to do that. 
**Update:** if you use –split-3 you will get three files, a left file, a right file, and a singletons file. Then you may not need to reorder your fastq files.


On linux:

export PATH=$PATH:/home/sandra/sratoolkit.2.10.9-ubuntu64/bin

prefetch --option-file ~/baby_woman.txt
