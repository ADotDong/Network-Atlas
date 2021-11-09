# Gene Transcriptional Regulator Network Atlas

### Constructing and analyzing transcriptional regulators networks
I downloaded 1066 ChIP-Seq files in BED (Browser Extensible Data) format, with the filter keyword of “broadpeak”, from five UCSC genomic data portals.

http://hgdownload.soe.ucsc.edu/goldenPath/hg19/encodeDCC/wgEncodeHaibTfbs/,
http://hgdownload.soe.ucsc.edu/goldenPath/hg19/encodeDCC/wgEncodeSydhHistone/
http://hgdownload.soe.ucsc.edu/goldenPath/hg19/encodeDCC/wgEncodeSydhTfbs/
http://hgdownload.soe.ucsc.edu/goldenPath/hg19/encodeDCC/wgEncodeUwHistone/ 
http://hgdownload.soe.ucsc.edu/goldenPath/hg19/encodeDCC/wgEncodeUwTfbs/.

Those BED files, produced by the ENCODE project, contain the genomic coordinates of transcriptional regulator binding sites on the assembled human genome (version hg19), produced by different ChIP-Seq experiments in a variety of cell lines. I pre-processed those downloaded BED files using a customized script that I wrote to merge the redundant genomic regions within a BED file into unique genomic regions, and sorted the genomic positions according to their chromosome and coordinantes in each BED file. I then sorted those BED files according to the sources of the cell lines. For some cell lines, only one or two ChIP-Seq experiments were performed. Since I wanted to explore large networks instead of small ones, I only restricted the subsequent analysis with 22 cell lines with at least 10 transcriptional regulators.

For all the BED files from the same cell line, I applied the GPSmatch program to calculate the Jaccard index to measure the similarity between every pair of BED files. Using the obtained pairwise Jaccard indices, I created a similarity matrix among all the transcriptional regulators in each cell line using customized R scripts that I wrote. Then, I applied the R package iGraph (Csardi et al, 2006) to the similarity matrix to construct weighted, undirected networks of transcriptional regulators using a threshold of Jaccard index value of 0.25. Finally, I identified network modules from the obtained networks using the following module identification algorithms implemented in the iGraph package: infomap, walktrap, edge_betweenness, fast_greedy, label_prop, leading_eigen, and louvain. to identify modules from the treatment network. Transcriptional factors within the same modules are more similar in terms of the underlying shared genomic-binding profiles than those between different modules, thereafter referred to as potential coordination networks. In addition to the network analysis, I also applied the R package corrgram to construct corrgrams to visualize the degrees of similarity of transcriptional regulators within the same cell line.

All the results can be download from this Github repository.
