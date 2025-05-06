# MyGenome
CS480G Genome Data Project

Use headings to highlight the individual procedures (# for top level, ## for second level)
Use numbers to list steps
identify code lines by placing them between lines with ```bash and ```

![MyGenomeNCBISub.png](/data/MyGenomeNCBISub.png)

Submission Portal: https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsubmit.ncbi.nlm.nih.gov%2Fsubs%2F&data=05%7C02%7Cnaca249g%40uky.edu%7C898af3c9c01c40b0a6a108dd4c682e0d%7C2b30530b69b64457b818481cb53d42ae%7C0%7C0%7C638750732503290272%7CUnknown%7CTWFpbGZsb3d8eyJFbXB0eU1hcGkiOnRydWUsIlYiOiIwLjAuMDAwMCIsIlAiOiJXaW4zMiIsIkFOIjoiTWFpbCIsIldUIjoyfQ%3D%3D%7C0%7C%7C%7C&sdata=pewpQexFtMknb%2B9lYcbON4YzE1CyfwmYvsHZ3PLzfJI%3D&reserved=0 (login required) 


MyGenome Class Metadata sheet information: 
For number of paired reads remaining after trimming:
zcat Bm88509_paired_1.fq.gz | grep -c "^@" = 7612219

For number of high quality nucleotides (R1 + R2)  reads: 
zcat Bm88509_paired_1.fq.gz | awk 'NR%4==2 {bases += length($0)} END {print bases}' 
+
zcat Bm88509_paired_2.fq.gz | awk 'NR%4==2 {bases += length($0)} END {print bases}'
= 2277218354

For the Total Genome Size, # of contigs, and N50 at step size 10:
I navigated in the UK MCC to the velvet optimizer log file created with my output directory. I then used nano to find the value in the "total", "N50", and "contigs" spots at the bottom of the LOG file. 
Total Genome Size = 41395274
Number of contigs = 5101
N50 = 197131

For the Total Genome Size at step size 2: 
Same as above but I navigated to the bottom of the step size 2 output directory LOG file. 
Total Genome Size = 40976953
Number of contigs = 2921
N50 = 212275

Fold Coverage: 54.00
After running BUSCO and looking at the reports, my BUSCO score was 98.4% which jumped up to 98.6% with the completed fragmented score.
For # of predicted proteins, I ran the following command line tool on my Bm88509-annotations.gff file I createdd in the maker directory on my VM: 

'''bash  awk ' BEGIN {count=0;} {if ($3 == "gene") count+=1} END{print count}' Bm88509-annotations.gff '''
Which gave me 12886 total. 

I then used: 
'''bash scp Bm88509-annotations.gff naca249@mcc.uky.edu:/project/farman_s25abt480/CLASS_GFFs/ '''
to copy the annotations.gff file to the CLASS_GFFs directory on the MCC. 





