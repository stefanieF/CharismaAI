# CharismaBERT
This repository holds the code for the conference talk on charisma signaling in crises situations by Krügl et al. presented at the EAWOP 2023 in Katowice, Poland <br />
The provided notebooks finetune multiple BERT models that predicts charismatic leadership tractics in text.<br />

## Abstract
### Real Leaders Emerge from Crises: 
### A Study on Female and Male Governors’ Charisma in Times of the COVID-19 Crises. 
Nowadays, one crisis chases the other, and that calls for strong leadership. But do leaders become more charismatic in times of crisis? Many scholars theorized crisis as an antecedent for leader charisma (e.g., Shamir, House, & Arthur, 1993; Shamir & Howell 1999). Bligh et al. (2004) demonstrated that U.S. President George W. Bush increased his charismatic rhetoric after 9/11, and classified it into eight “charismatic themes” (See Shamir et al., 1994).
Bastardoz et al. (2022) expanded their results: They showed that a crisis does not only foster “charismatic themes” (Shamir et al., 1994), but also the amount of charismatic leadership tactics (CLTs) (Antonakis et al., 2011) in presidential speeches. They used a Regression Discontinuity in Time (RDiT) design to identify the causal effects. They extended generalizability, by examining the speeches of French President François Hollande after the 2015 Paris attacks. However, both studies focused on terrorist attacks, sampled few speakers and focused solely on male leaders. 
Our study analyzes the rhetoric of 9 female and 9 male U.S. governors 3 months before and after the onset of the COVID-19 pandemic. We thereby extend previous insights of charisma and crises literature in at least three ways: Firstly, we explore leader gender as a moderator of the relationship between crisis and leader charisma. Secondly, we explore the nature of a different crises (e.g., terror attacks vs. pandemic). Thirdly, we sampled more speakers. 
### Theoretical Background
Antonakis et al. (2016, p. 304) defined charisma as “values-based, symbolic, and emotion-laden leader signaling”.  We suggest: (H1) crisis will increase the amount of verbal CLTs used by political leaders. 
According to role congruity theory (Eagly & Karau, 2002), we suggest that women (1) often do not fit the leader stereotype and (2) are criticized for not behaving like women when acting as agentic leaders. Consequently, female and male leaders could also craft their speeches to match gender stereotypes. Hence, we explore:
- RQ1: Do female and male political leaders use different CLTs?
- RQ2: Does the use of CLTs change as a function of politicians’ gender and crisis?
### Study Design (Data collection finished by April 2023)
We selected 9 female U.S. governors and utilized a propensity score matching to find 9 statistically identical male U.S. governors. Following Bastardoz et al. (2022), we used a RDiT approach, and centered our assignment variable on 15 March 2020 where the “Declaration of a National Emergency” marked the onset of the crisis in the USA (measurement period: December 15, 2019 - June 15, 2020). We are collecting a sample of 14 speeches (7 before / 7 after the assignment variable) for each governor (n=252). Speeches are assigned to variable treatment based on time (i.e., assignment variable) and declaration of state of emergency (i.e., discontinuity). The sum of CLTs and the individual tactics within a speech represent the dependent variables. We examine the influence of gender as a moderator and control for both the total number of words and sentences within a speech (data analysis ongoing).
### Results expected
We anticipate that the crisis will increase the use of CLTs. In addition, we do not expect significant gender differences in the frequency of CLT use, but for the type of CLTs used.
### Limitations 
Since more female governors are Democrats, our sample is unbalanced between the parties. Democratic states had stricter Corona regulations than Republican states, which has an impact on the rhetoric and perceptions of the Corona crisis.
Future research could conduct a more nuanced analysis of gender differences in the use of agency and community tactics with a more balanced sample.
### Implications
Our research expands knowledge on how crises affect charisma signaling, which is crucial for responsible political leaders’ communication in the face of rising global crises.
We also show whether women use the same amount and types of CLTs as men and examine the impact of gender stereotypes in crisis communication.
### Congress Theme (the future is now: the changing world of work)
Crises exist in all areas - both global crises (e.g., climate change) and organizational crises (e.g., corporate restructuring) - and will challenge future leaders. Analyzing the rhetoric of female and male leaders during crises can help to improve future crisis communication in all fields.
### UN SDGs
Gender equality and Decent work and economic growth


## Data and training methods

- The models are trained on annotated governor speeches. Details for the annotations can be found under . 
- We use the VUA metaphor corpus for training the model responsible for tagging the use of metaphors by Steen et al. 2010
- To train the models for the other tactics we use gpt3.5 (Brown et al. 2021) to generate corpora containing sentences with the tactics.
- As of 2023-05-17 we generated a corpus for the tactic "moral conviction" by using a moral words dictionary by Graham et al. 2012.
- In the following weeks we will update the models by generating more corpora for the other tactics.

## Model performance and inference

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


### Literature<br />
- Antonakis, J., Bastardoz, N., Jacquart, P., & Shamir, B. (2016). Charisma: An ill-defined and ill-measured gift. Annual Review of Organizational Psychology and Organizational Behavior, 3, 293-319. <br />
- Antonakis, J., Fenley, M., & Liechti, S. (2011). Can charisma be taught? Tests of two interventions. Academy of Management Learning & Education, 10(3), 374-396.<br />
- Bligh, M. C., Kohles, J. C., & Meindl, J. R. (2004). Charisma under crisis: Presidential leadership, rhetoric, and media responses before and after the September 11th terrorist attacks. The Leadership Quarterly, 15(2), 211-239.<br />
- Bastardoz, N., Jacquart, P. & Antonakis, J. (2022). Effect of crises on charisma signaling: A regression discontinuity design. The Leadership Quarterly, 101590. <br />
- Eagly, A. H., & Karau, S. J. (2002). Role congruity theory of prejudice toward female leaders. Psychological review, 109(3), 573.<br />
- Jensen, U., Rohner, D., Bornet, O., Carron, D., Garner, P., Loupi, D., & Antonakis, J. (2021, February 10). Combating COVID-19 with Charisma: Evidence on Governor Speeches and Physical Distancing in the United States. https://doi.org/10.31234/osf.io/ypqmk<br />
- Shamir, B., Arthur, M. B., & House, R. J. (1994). The rhetoric of charismatic leadership: A theoretical extension, a case study, and implications for research. The Leadership Quarterly, 5(1), 25-42.<br />
- Shamir, B., House, R. J., & Arthur, M. B. (1993). The motivational effects of charismatic leadership: A self-concept based theory. Organization Science, 4(4), 577-594.<br />
- Shamir, B., & Howell, J. M. (1999). Organizational and contextual influences on the emergence and effectiveness of charismatic leadership. The Leadership Quarterly, 10(2), 257-283.<br />
- Steen, G.J., Dorst A.G., Herrmann, J.B., Kaal, A.A., Krennmayr, T., Pasma, T. (2010). A method for linguistic metaphor identification. From MIP to MIPVU. Amsterdam: John Benjamins. <br />
- T. B. Brown et al., “Language Models are Few-Shot Learners.” arXiv, 2020. doi: 10.48550/ARXIV.2005.14165 <br />
- Graham, J., & Haidt, J. (2012). The moral foundations dictionary. Available at: http://moralfoundations.org <br />
