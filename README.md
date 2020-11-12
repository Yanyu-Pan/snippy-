# snippy-笔记
snippy-clean_full_aln core.full.aln > clean.full.aln  
run_gubbins.py -p gubbins --threads 10 -f 44 clean.full.aln 
snp-sites -c -o clean.core.aln gubbins.filtered_polymorphic_sites.fasta 
iqtree -s clean.core.aln -m MFP+ASC -bb 1000 -bnni -cmax 10 -nt 10 或 FastTree -gtr -nt clean.core.aln > clean.core.tree 
查看gubbins去重组后的core gene中各菌株与ref对比的等位基因数量  
思路：把clean.core.aln再运行一遍snippy 
第一步 批量把clean.core.aln中各菌的core seq批量提出来，分别保存 
awk '/^>/ { print n $0; n = "" } END { printf "%s", n }' clean.core.aln >list
然后整理list为仅含有菌株名称
第二步批量提取
for i in `cat list`
do
awk '/'$i'/{getline a;print $0"\n"a}'> $i.fasta
然后继续snippy-muti啥的
