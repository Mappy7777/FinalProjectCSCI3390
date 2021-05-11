# Large Scale Data Processing: Final Project
## Graph matching
For the final project, you are provided 6 CSV files, each containing an undirected graph, which can be found [here](https://drive.google.com/file/d/1khb-PXodUl82htpyWLMGGNrx-IzC55w8/view?usp=sharing). The files are as follows:  

|        Graph file             |  Number of edges  |   Number of Matchings   | run time |Computational power
| ------------------------------| ----------------- |-----------------|------------------ |--------------    
| log_normal_100.csv            | num         |        num      | enter         | compute
| musae_ENGB_edges.csv          | num          |        num      | enter       | compute
| soc-pokec-relationships.csv   | num          |        num      | enter      | compute
| soc-LiveJournal1.csv          | num          |        num      | enter     | compute
| twitter_original_edges.csv    | num            |        num      | enter       | compute
| com-orkut.ungraph.csv         | enter             |        num      | enter      | compute

## Our Approach
Our initial approach was to use a non vertex-centric algorithm to find the maximal matching, as this would have a very fast runtime. However, we were having significant issues making out own partitioner and we also realized we did not need our algorithm to be that fast. After testing out nonvertex-centric approaches we finally decided to implement a variation of the Israeli-Itai algorithm. We couldn't figure out a way to implement the original algorithm in apex, but came up with a variation that ran in constant rounds and produced an ok estimate of the maximal matching. 

