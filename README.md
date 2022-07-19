# Quantify the yearly gender bias in RoBERTa and GPT-2

## Introduction

This is a WIP.

Bias quantification for large NLP models have attracted wide interest. Conflicting results have been reported. To provide an alternative perspective, I focus on the intermediate pre-training checkpoints. Intuitively, models should gradually pick up the bias during the pre-training process. The process is expected to be monotonous.

In the first version, I planned to measure the bias across years, hence the repository name.

## Related Work

### Pre-trained Checkpoints

The intermediate checkpoints during the pre-training process have been released for [BERT](https://openreview.net/pdf?id=K0E_F0gFDgA), [RoBERTa](https://aclanthology.org/2021.findings-emnlp.71.pdf), and [GPT-2 small and medium](https://crfm.stanford.edu/2021/08/26/mistral.html). One previous work also considers [ALBERT](https://aclanthology.org/2020.emnlp-main.553.pdf), but the checkpoints are not released yet. Despite the checkpoints not released, all large models inevitably involve the pre-training step. There are also some related works for smaller models, such as [LSTM](https://aclanthology.org/N19-1329.pdf).

### Gender Biases in NLP

There are bias-oriented [workshops](https://aclanthology.org/volumes/2022.gebnlp-1/). 

For more details, refer to [this survey](https://arxiv.org/abs/2112.14168) of 304 papers, mentioned by this [paper](https://aclanthology.org/2022.gebnlp-1.3.pdf).

## The Pre-Trained Checkpoints

### Quantification

The step-interval of pre-training models are not uniform, and it differ for models. The length of the pre-training, measured by epochs, also differs for all models.

The total number of released full pre-training processes are fewer than 20. The total number of different random seeds used is also less than 100.

### Previous Findings

Some has discovered that the commonsense knowledge has been relearned during the pre-training process.

## Experimental Setup

### The Template

I have adopted the common template of "[PRONOUN] is a [PROFESSION]". I also try the alternative of using the profession as the subject and an adjective (either male or female) as the object. The latter template has resulted in lower absolute scores (around 1e-5 for both tokens) than the former setting (around 1e-2 for both tokens). Even with the former setting, I am not able to achieve the around 30% absolute score as reported by [Delobelle et al., 2022](https://aclanthology.org/2022.naacl-main.122).

### The Ratio

I follow the conventional way of comparing the ratios of the gender related tokens. The prior has not been removed from the analysis, so it could be expected that the absolute value of the male token would usually be higher than the female token, even for stereotypic female jobs.

### Yearly Bias

In the first version repository, I try to quantify the yearly gender bias by including a year in the prompt. For example, the full sentence is "In 1992, a doctor is a \<mask\>.", where the masked word is chosen from "male" and "female" in the most common binary setting. The ratio between the probabilities are plotted against the year, currently 1900-2022. 

I also tried to add the month name before the year ("In January 1992, ..."). In other words, the total list of prompts is twelve times longer than the original list with only the year injected. This has created some very interesting artifacts. Please see the notebooks for details. I randomly choose 4 occupations with a consonant as the beginning to match the determiner "a", and the results turned out to be very different.

Currently only the RoBERTa version has been implemented as a proof-of-concept.

### Correlation Tests

The correlations are tested and plotted similarly as in [Delobelle et al., 2022](https://aclanthology.org/2022.naacl-main.122).

## Results and Discussion

### Instability of Yearly Trends

As shown in the videos, sometimes conflicting trends develop over the pre-training process. 

### Correlation Stripes

This indicate that some intermediate checkpoints are very different from others.

### The Entropy

I hypothesize that the tokens with lower absolute score will be less stable than highly-probable tokens during the pre-training process. Thus, I try to plot the entropy calculated on all tokens during the pre-training process. Though the analysis has not yet arrived at a conclusion, I observe that the entropy for sentences containing a more recent year has resulted in a higher entropy.

## Conclusion

TBA.

## References

TBA.

Measuring Fairness with Biased Rulers: A Comparative Study on Bias Metrics for Pre-trained Language Models ([Delobelle et al., 2022](https://aclanthology.org/2022.naacl-main.122))
