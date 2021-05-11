# Large Scale Data Processing: Final Project
## Graph matching
For the final project, you are provided 6 CSV files, each containing an undirected graph, which can be found [here](https://drive.google.com/file/d/1khb-PXodUl82htpyWLMGGNrx-IzC55w8/view?usp=sharing). The files are as follows:  

|        Graph file             |  Number of edges  |   Number of Matchings   | run time |Computational power
| ------------------------------| ----------------- |-----------------|------------------ |--------------    
| log_normal_100.csv            | 2671        |        12      | 1s         | 1x1 cores (ran locally)
| musae_ENGB_edges.csv          | 35324         |        975      | 1s       | 1x1 cores (ran locally)
| soc-pokec-relationships.csv   | 22301964          |        271114      | 86s      | 2x4 N1 cores 
| soc-LiveJournal1.csv          | 42851237         |        757074      | 112s     | 2x4 N1 cores
| twitter_original_edges.csv    | 63555749           |        52197      | 146s       | 2x4 N1 cores
| com-orkut.ungraph.csv         | 117185083             |        523525      | 192s      | 2x4 N1 cores

## Our Approach
Our initial approach was to use a non vertex-centric algorithm to find the maximal matching, as this would have a very fast runtime. However, we were having significant issues making out own partitioner and we also realized we did not need our algorithm to be that fast. After testing out nonvertex-centric approaches we finally decided to implement a variation of the Israeli-Itai algorithm. We couldn't figure out a way to implement the original algorithm in apex, but came up with a variation that ran in constant rounds and produced an ok estimate of the maximal matching. 

