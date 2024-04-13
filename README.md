# assignment_3_sample_data

The `data` folder contains 3 files:

* The `input.txt.gz` is the input file in the format discussed in the specification. Make sure to unzip it before you process it.

* The `true_counts.tsv` file contains the ground truth number of reads coming from each transcript.

* The `ref_quant.tsv` file contains the estimated counts arising from the reference EM solution.

In this example, the true counts and ref quants have a spearman correlation of ~0.68 and a pearson correlation of ~0.97.  This is 
low (in spearman) mostly because the read depth is low.  However, this is about what you should be aiming for in terms of the accuracy 
of your solution.


