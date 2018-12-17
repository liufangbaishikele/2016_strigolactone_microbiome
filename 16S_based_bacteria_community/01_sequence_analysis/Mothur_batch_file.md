make.contigs(inputdir=/staton/projects/soybean_rhizosphere/2016_strigolactone/ITS_2016_strigolactone/00_raw_fastq,outputdir=/staton/projects/soybean_rhizosphere/2016_strigolactone/ITS_2016_strigolactone/01_mothur,file=ST.file,oligos=ST.oligo,processors=36)

summary.seqs(inputdir=/staton/projects/soybean_rhizosphere/2016_strigolactone/ITS_2016_strigolactone/01_mothur,fasta=ST.trim.contigs.fasta,processors=36)

screen.seqs(fasta=ST.trim.contigs.fasta,group=ST.contigs.groups,maxambig=0,maxlength=462,processors=24)

summary.seqs(fasta=ST.trim.contigs.good.fasta,processors=24)

unique.seqs(fasta=ST.trim.contigs.good.fasta)

count.seqs(name=ST.trim.contigs.good.names,group=ST.contigs.good.groups)

summary.seqs(count=ST.trim.contigs.good.count_table,processors=24)

pre.cluster(fasta=ST.trim.contigs.good.unique.fasta,count=ST.trim.contigs.good.count_table,diffs=3,processors=24)

chimera.vsearch(fasta=ST.trim.contigs.good.unique.precluster.fasta,count=ST.trim.contigs.good.unique.precluster.count_table,dereplicate=t,processors=24)

remove.seqs(fasta=ST.trim.contigs.good.unique.precluster.fasta,accnos=ST.trim.contigs.good.unique.precluster.denovo.vsearch.accnos,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.count_table)

summary.seqs(fasta=ST.trim.contigs.good.unique.precluster.pick.fasta,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.count_table,processors=24)

classify.seqs(fasta=ST.trim.contigs.good.unique.precluster.pick.fasta,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.count_table,reference=UNITEv6_sh_97.fasta,taxonomy=UNITEv6_sh_97.tax,cutoff=80,processors=24)

remove.lineage(fasta=ST.trim.contigs.good.unique.precluster.pick.fasta,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.count_table,taxonomy=ST.trim.contigs.good.unique.precluster.pick.UNITEv6_sh_97.wang.taxonomy,taxon=unknown)

summary.tax(taxonomy=ST.trim.contigs.good.unique.precluster.pick.UNITEv6_sh_97.wang.pick.taxonomy,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table)

pairwise.seqs(fasta=ST.trim.contigs.good.unique.precluster.pick.pick.fasta,cutoff=0.1,align=needleman,output=lt,countends=T,calc=onegap,processors=24)

cluster(phylip=ST.trim.contigs.good.unique.precluster.pick.pick.phylip.dist,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table,method=opti,cutoff=0.03,processors=24)


make.shared(list=ST.trim.contigs.good.unique.precluster.pick.pick.phylip.opti_mcc.list,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table,label=0.03)

classify.otu(list=ST.trim.contigs.good.unique.precluster.pick.pick.phylip.opti_mcc.list,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table,taxonomy=ST.trim.contigs.good.unique.precluster.pick.UNITEv6_sh_97.wang.pick.taxonomy,label=0.03)

*Phylotype based clustering*

phylotype(taxonomy=ST.trim.contigs.good.unique.precluster.pick.UNITEv6_sh_97.wang.pick.taxonomy)

make.shared(list=ST.trim.contigs.good.unique.precluster.pick.UNITEv6_sh_97.wang.pick.tx.list,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table,label=1)

classify.otu(list=ST.trim.contigs.good.unique.precluster.pick.UNITEv6_sh_97.wang.pick.tx.list,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table,taxonomy=ST.trim.contigs.good.unique.precluster.pick.UNITEv6_sh_97.wang.pick.taxonomy,label=1)


*Doing clustering based on vsearch developed greedy clustering method first, and set up the cutoff to 0.03 as the generated list file will be OTU with 97% similarity.* 
 
*cluster(fasta=ST.trim.contigs.good.unique.precluster.pick.pick.fasta,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table,method=dgc,cutoff=0.03,processors=48)

*make.shared(list=ST.trim.contigs.good.unique.precluster.pick.pick.dgc.list,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table,label=0.03)

*classify.otu(list=ST.trim.contigs.good.unique.precluster.pick.pick.dgc.list,count=ST.trim.contigs.good.unique.precluster.denovo.vsearch.pick.pick.count_table,taxonomy=ST.trim.contigs.good.unique.precluster.pick.UNITEv6_sh_97.wang.pick.taxonomy,label=0.03)
