# Large Scale Data Processing: Final Project
## Graph matching
For the final project, you are provided 6 CSV files, each containing an undirected graph, which can be found [here](https://drive.google.com/file/d/1khb-PXodUl82htpyWLMGGNrx-IzC55w8/view?usp=sharing). The files are as follows:  

|        Graph file             |  Number of edges  |   Number of Matchings   | run time |Compute
| ------------------------------| ----------------- |-----------------|------------------ |--------------    
| log_normal_100.csv            | 2671        |        12      | 1s         | 1x1 cores (ran locally)
| musae_ENGB_edges.csv          | 35324         |        975      | 1s       | 1x1 cores (ran locally)
| soc-pokec-relationships.csv   | 22301964          |        271114      | 86s      | 2x4 N1 cores GCP
| soc-LiveJournal1.csv          | 42851237         |        757074      | 112s     | 2x4 N1 cores GCP
| twitter_original_edges.csv    | 63555749           |        52197      | 146s       | 2x4 N1 cores GCP
| com-orkut.ungraph.csv         | 117185083             |        523525      | 192s      | 2x4 N1 cores GCP

## Our Approach
Our initial approach was to use a non vertex-centric algorithm to find the maximal matching, as this would have a very fast runtime. However, we were having significant issues making out own partitioner and we also realized we did not need our algorithm to be that fast. After testing out nonvertex-centric approaches we finally decided to implement a variation of the Israeli-Itai algorithm. We couldn't figure out a way to implement the original algorithm in apex, but came up with a variation that ran in constant rounds and produced an ok estimate of the maximal matching. The way our approach works is each active vertex proposes to a random neighbor.Every active vertex will then accept a proposal with probability P = x/(x+y), as was suggested in the discussion. In this case x is the value of a given vertex and y and the value of it's neighbor. Each active vertex then randomly generates a 0 or 1. The proposed edge from u to v will join M if u generated 0 and v generated 1. We then deactivate all of the edges in M. This will run until there are no more active vertices. A problem we ran into was that our algorithm would always stop after 1 iteration. We are still unsure of why this is happening, it could be a simple syntax error but we were unable to fix it in time. Despite running only one iteration, we were able to get an ok estimate on the maximal matching of the graphs. If we were to recieve a new test case, we would initially try to run a fixed version of our algorithm. If runtime were a primary concern we would run one of the nonvertex-centric models.

## Advantages 
Our algorithm runs appears to run in constant rounds which is extremely good. We are unable to prove this though as this is happening on accident. The Israeli-Itai algorithm is supposed to run in O(logn) rounds which is already good, but our algorithm finished in 1 round for all of the datasets. Since it runs in only one rounds it is unlikley that it achieves a 1/2-approximation ratio. The Israeli-Itai algorithm achieves this, but it runs in O(logn) rounds. If we were to guess it probably produces a O(1/logn)x(1/2) approximation ratio. But, it was impossible for us to prove this as our algorithm runs in 1 round by accident.
references:Israeli, A. Itai, "A Fast and Simple Randomized Parallel Algorithm for Maximal Matching"

