# Quantify the yearly gender bias in RoBERTa and GPT-2

In this repository, I try to quantify the yearly gender bias by including a year in the prompt. For example, the full sentence is "In 1992, a doctor is a \<mask\>.", where the masked word is chosen from "male" and "female" in the most common binary setting. The ratio between the probabilities are plotted against the year, currently 1900-2022. 

I also tried to add the month name before the year ("In January 1992, ..."). In other words, the total list of prompts is twelve times longer than the original list with only the year injected. This has created some very interesting artifacts. Please see the notebooks for details. I randomly choose 4 occupations with a consonant as the beginning to match the determiner "a", and the results turned out to be very different.

Currently only the RoBERTa version has been implemented as a proof-of-concept.
