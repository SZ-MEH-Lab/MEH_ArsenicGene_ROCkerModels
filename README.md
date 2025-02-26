# MEHTool_ArsenicGene_ROCkerModels
This repository contains As-related gene databases and ROCker models, including aioA, arxA, arrA, arsC1, arsC2, arsM, arsI, and arsP genes. If you have any other questions or needs related to the ROCker models, please don't hesitate to contact us (syzhang@des.ecnu.edu.cn). The databases and ROCker models provided here may only be used for academic exchange and are not permitted for commercial use.

If you use the databases or ROCker models of aioA, arxA, arrA, arsC1, and arsC2 genes, please cite the paper at Microbiome (https://doi.org/10.1186/s40168-024-01952-4).
If you use the databases or ROCker models of arsM, arsI, and arsP genes, please cite the paper at Environ Sci Technol (https://doi.org/10.1021/acs.est.4c08620).

# Citation
Zhao, XD., Gao, ZY., Peng, JJ. et al. Various microbial taxa couple arsenic transformation to nitrogen and carbon cycling in paddy soils. Microbiome 12, 238 (2024).
Gao, ZY., Zhao, XD., Chen, Chuan. et al. Paddy Soil Flooding and Nonflooding Affect the Transcriptional Activity of Arsenic Methylation and Demethylation Communities. Environ Sci Technol (2025).

# Usage
# Setp1: compute BLAST file.
1) Method 1:  Execute ROCker search. The minimum required parameters are:
> singularity exec ROCker.sif ROCker search -q input.fasta -k model.rocker -o output.blast
Where input.fasta is the input metagenome in FastA format, model.rocker is the ROCker model(eg. aioA.150.rocker.txt), and output.blast is the output file to be created in tabular BLAST format. Similarity search algorithm including 'blast' and 'diamond' are supported, you can use "--search diamond (or blast)" to define. For additional supported options, execute singularity exec ROCker.sif ROCker search -h. (Please install ROCker.sif before use according to http://enve-omics.ce.gatech.edu/rocker/) 

2) Method 2: You can use the software 'blast' or 'diamond' to compute BLAST file.
> diamond blastx -q input.fasta -o output.blast -d db.dmnd -f 6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore qlen slen qcovhsp scovhsp
or
> blastx -query input.fasta -out output.blast -db db.fasta blastp -db $DB -query $input -out $output -outfmt "6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore qlen slen qcovs"
Where input.fasta is the input metagenome in FastA format, output.blast is the output file to be created in tabular BLAST format, db.dmnd (eg. aioA_ROCker.ref.dmnd) and db.fasta (eg. aioA_ROCker.ref.fa) are the corresponding ROCker database.

# Note: If you have a pre-computed BLAST file, you can execute Setp2 directly.
# Setp2:  Execute ROCker filter. The minimum required parameters are:
> singularity exec ROCker.sif ROCker filter -x input.blast -k model.rocker -o output.blast 
Where input.blast is the input search to be filtered in tabular BLAST format, model.rocker is the ROCker model (eg. aioA.150.rocker.txt), and output.blast is the output file to be created in tabular BLAST format (you can use this file to do further analysis). For additional supported options, execute singularity exec ROCker.sif ROCker filter -h.

# If you want to know more infomation about ROCker, please read the paper at Nucleic Acids Res (https://doi.org/10.1093/nar/gkw900).
