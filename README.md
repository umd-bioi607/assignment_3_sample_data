# assignment_3_sample_data

The `data` folder contains 3 files:

* The `input.txt.gz` is the input file in the format discussed in the specification. Make sure to unzip it before you process it.

* The `true_counts.tsv` file contains the ground truth number of reads coming from each transcript.

* The `ref_quant.tsv` file contains the estimated counts arising from the reference EM solution.

In this example, the true counts and ref quants have a spearman correlation of ~0.68 and a pearson correlation of ~0.97.  This is 
low (in spearman) mostly because the read depth is low.  However, this is about what you should be aiming for in terms of the accuracy 
of your solution.

To compute these correlations above, very small predicted values were first truncated to 0.  You can use the snippet of code below to compute your 
estimates' correlation with the truth:

```python
def get_metrics(truth, pred):
  # truncate small values
  y = pd.read_csv(pred, sep='\t')
  y.loc[(y.est_frag < 1e-8), 'est_frag'] = 0

  x = pd.read_csv(truth, sep='\t')
  m = pd.merge(x, y, left_on='name', right_on='name', how='outer')
  metrics = {}
  for ctype in ["spearman", "pearson"]:
    metrics[ctype] = m[['est_frag', 'true_count']].corr(method=ctype)['est_frag']['true_count']
  return metrics
```
