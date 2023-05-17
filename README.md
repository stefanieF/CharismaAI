# CharismaBERT
This repository holds the code for the conference talk on charismatic behaviour by Krügl et al. [1] <br />
The provided notebooks fine tune multiple BERT models that predicts charismatic leadership tractics in text.<br />
The charismatic tactics are:<br />
Metaphor/Simile, rhetorical question, stories/anecdotes, contrast, lists, repetition, moral conviction, sentiment of the collective, setting high expectations and confidence in goals 
### Data and training methods:

- The models are trained on annotated governor speeches. Details for the annotations can be found under [1]. 
- We use the VUA metaphor corpus for training the model responsible for tagging the use of metaphors. [2]
- To train the models for the other tactics we use gpt3.5 [3] to generate corpora containing sentences with the tactics.
- As of 2023-05-17 we generated a corpus for the tactic "moral conviction" by using a moral words dictionary [4]
- In the following weeks we will update the models by generating more corpora for the other tactics.

### Model performance and inference

- For the inference of all tactics we use a two-step model.
  - Firstly we predict whether any charismatic tactic is present in the sentence
  - Secondly we iterate over the tactics and predict whether the tactic is present in the sentence
- The model performances as of 2023-05-17 are summarized in the table below:

| with corpus    |                 |          |                  |                     |        |                     |          |                   |      |            |                             |                           |
|----------------|-----------------|----------|------------------|---------------------|--------|---------------------|----------|-------------------|------|------------|-----------------------------|---------------------------|
| Model          | Charisma Tactic | Metaphor | Moral conviction | Rhetorical question | Simile | confidence in goals | Contrast | Stories/Anecdotes | List | Repetition | Sentiment of the collective | Setting high expectations |
| Accuracy       | -               |     95,6 |             85,1 |                     |        |                     |          |                   |      |            |                             |                           |
| Precision      | -               |     96,8 |             90,3 |                     |        |                     |          |                   |      |            |                             |                           |
| F1-Score       | -               |     95,4 |             90,5 |                     |        |                     |          |                   |      |            |                             |                           |
| without corpus |                 |          |                  |                     |        |                     |          |                   |      |            |                             |                           |
| Model          | Charisma Tactic | Metaphor | Moral conviction | Rhetorical question | Simile | confidence in goals | Contrast | Stories/Anecdotes | List | Repetition | Sentiment of the collective | Setting high expectations |
| Accuracy       |            73,0 |     95,6 |             73,9 |                99,5 |   99,6 |                94,7 |     89,0 |              97,0 | 92,9 |       80,0 |                        92,7 |                      89,0 |
| Precision      |            78,4 |     37,5 |             79,1 |                84,2 |   50,0 |                64,5 |     51,4 |              65,1 | 80,6 |       65,8 |                        98,7 |                      56,8 |
| F1-Score       |            78,2 |     25,5 |             78,9 |                88,9 |   50,0 |                48,8 |     44,9 |              54,4 | 78,4 |       62,7 |                        38,3 |                      53,5 |
<br />
<br />

This work is based on the DeepEthics Framework by Banks et al. The code can be found under: https://github.com/atefehmah/DeepEthics <br />
The corresponding paper for this work is found under: https://doi.org/10.1016/j.leaqua.2022.101658 <br />
<br />
[1] EAWOP citation  <br />
[2] Steen, G.J., Dorst A.G., Herrmann, J.B., Kaal, A.A., Krennmayr, T., Pasma, T. (2010). A method for linguistic metaphor identification. From MIP to MIPVU. Amsterdam: John Benjamins. <br />
[3] T. B. Brown et al., “Language Models are Few-Shot Learners.” arXiv, 2020. doi: 10.48550/ARXIV.2005.14165 <br />
[4] Graham, J., & Haidt, J. (2012). The moral foundations dictionary. Available at: http://moralfoundations.org <br />
