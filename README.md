# ML_BCP
Machine learning techniques for personalized breast cancer risk prediction

This Collaborative research project develops methods, validates tools, and disseminates machine learning techniques for personalized breast cancer risk prediction (**ML_BCP**). The techniques are compared against state-of-the-art model-based approaches like [Breast Cancer Risk Assessment Tool (BCRAT)](https://bcrisktool.cancer.gov) and [Breast and Ovarian Analysis of Disease Incidence and Carrier Estimation Algorithm (BOADICEA)](https://ccge.medschl.cam.ac.uk/boadicea/).

Table of contents
=================

<!--ts-->
   * [Table of contents](#table-of-contents)
   * [Overview](#overview)
   * [Resources](#resources)
   * [Usage](#usage)
   * [Contact](#contact)
   * [References](#references)
<!--te-->


Overview
========

* *Background*: Breast cancer risk prediction modeling allows researchers to identify high-risk patients and reduce unnecessary interventions. Currently, breast cancer risk prediction models tend to exhibit low discriminatory accuracy (0.53-0.64). We are employing machine learning (ML) approaches to address current limitations and improve accuracy of outcome forecasts. This study compares the discriminatory accuracy of ML-based estimates against a pair of established methods: [Breast Cancer Risk Assessment Tool (BCRAT)](https://bcrisktool.cancer.gov) and [Breast and Ovarian Analysis of Disease Incidence and Carrier Estimation Algorithm (BOADICEA)](https://ccge.medschl.cam.ac.uk/boadicea/).

* *Methods*: Eight simulated datasets and two retrospective samples were used to compare the performance of the proposed ML methods against state-of-the-art BCRAT and BOADICEA models.

* *Results* : Predictive accuracy (AU-ROC curve) reached 88.28% using ML-Adaptive Boosting and 88.89% using ML-random forest versus 62.40% with BCRAT for the U.S. population-based sample. Predictive accuracy reached 90.17% using ML-adaptive boosting and 89.32% using ML-Markov chain Monte Carlo generalized linear mixed model versus 59.31% with BOADICEA for the Swiss clinic-based sample.

* *Conclusions*: The significant prediction improvement of the accuracy of classification of women with and without breast cancer achieved with ML algorithms is important in personalized medicine and may suggest prevention strategies and individualized clinical management.


Resources
=========

* [Data](https://github.com/SOCR/ML_BCP/tree/master/data)
* [Source-code (R-scripts)](https://github.com/SOCR/ML_BCP/tree/master/code)
* [Results](https://github.com/SOCR/ML_BCP/tree/master/results)

Usage
=====

Open Science


Contact
=======

* [Chang Ming](https://nursing.unibas.ch/de/personen/chang-ming/) and [Maria C. Katapodi](https://nursing.unibas.ch/de/personen/maria-katapodi/), [University of Basel](https://nursing.unibas.ch/de/home/)
* [Ivo D. Dinov](http://www.socr.umich.edu/people/dinov/), [SOCR](http://socr.umich.edu/)


References
==========
**Ming, C, Viassolo, V, Probst-Hensch, N, Chappuis, PO, Dinov, ID, and Katapodi, MC. (2019) [Machine learning techniques for personalized breast cancer risk prediction: comparison with the BCRAT and BOADICEA models](https://doi.org/10.1186/s13058-019-1158-4), Breast Cancer Research 21(1):75, DOI [10.1186/s13058-019-1158-4](https://doi.org/10.1186/s13058-019-1158-4).**

1.	Nelson HD, Tyne K, Naik A, Bougatsos C, Chan BK, Humphrey L. Screening for breast cancer: an update for the U.S. Preventive Services Task Force. Annals of internal medicine. 2009;151(10):727-37, w237-42.
2.	Arie S. Switzerland debates dismantling its breast cancer screening programme. BMJ : British Medical Journal. 2014;348.
3.	Christine Bouchardy PP, Matthias Lorez, Kerri Clough-Gorr, Andrea Bordoni and the NICER Working Group. Trends in Breast Cancer 
Survival in Switzerland. NICER. 2011;Schweizer Krebsbulletin(Nr. 4/2011).
4.	Mainiero MB, Moy L, Baron P, Didwania AD, diFlorio RM, Green ED, et al. ACR Appropriateness Criteria((R)) Breast Cancer Screening. Journal of the American College of Radiology : JACR. 2017;14(11s):S383-s90.
5.	Qin X, Tangka FK, Guy GP, Jr., Howard DH. Mammography rates after the 2009 revision to the United States Preventive Services Task Force breast cancer screening recommendation. Cancer causes & control : CCC. 2017;28(1):41-8.
6.	Sardanelli F, Aase HS, Alvarez M, Azavedo E, Baarslag HJ, Balleyguier C, et al. Position paper on screening for breast cancer by the European Society of Breast Imaging (EUSOBI) and 30 national breast radiology bodies from Austria, Belgium, Bosnia and Herzegovina, Bulgaria, Croatia, Czech Republic, Denmark, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Italy, Israel, Lithuania, Moldova, The Netherlands, Norway, Poland, Portugal, Romania, Serbia, Slovakia, Spain, Sweden, Switzerland and Turkey. European radiology. 2017;27(7):2737-43.
7.	King MC, Levy-Lahad E, Lahad A. Population-based screening for BRCA1 and BRCA2: 2014 Lasker Award. Jama. 2014;312(11):1091-2.
8.	Azim HA, Jr., Partridge AH. Biology of breast cancer in young women. Breast cancer research : BCR. 2014;16(4):427.
9.	Rosenberg SM, Newman LA, Partridge AH. Breast Cancer in Young Women: Rare Disease or Public Health Problem? JAMA oncology. 2015;1(7):877-8.
10.	Autier P, Boniol M. Mammography screening: A major issue in medicine. European journal of cancer (Oxford, England : 1990). 2018;90:34-62.
11.	van Ravesteyn NT, Miglioretti DL, Stout NK, Lee SJ, Schechter CB, Buist DS, et al. Tipping the balance of benefits and harms to favor screening mammography starting at age 40 years: a comparative modeling study of risk. Annals of internal medicine. 2012;156(9):609-17.
12.	Eccles SA, Aboagye EO, Ali S, Anderson AS, Armes J, Berditchevski F, et al. Critical research gaps and translational priorities for the successful prevention and treatment of breast cancer. Breast cancer research : BCR. 2013;15(5):R92.
13.	Maas P, Barrdahl M, Joshi AD, Auer PL, Gaudet MM, Milne RL, et al. Breast Cancer Risk From Modifiable and Nonmodifiable Risk Factors Among White Women in the United States. JAMA oncology. 2016;2(10):1295-302.
14.	Mandelblatt JS, Cronin KA, Bailey S, Berry DA, de Koning HJ, Draisma G, et al. Effects of mammography screening under different screening schedules: model estimates of potential benefits and harms. Annals of internal medicine. 2009;151(10):738-47.
15.	Pashayan N, Duffy SW, Chowdhury S, Dent T, Burton H, Neal DE, et al. Polygenic susceptibility to prostate and breast cancer: implications for personalised screening. British Journal of Cancer. 2011;104(10):1656-63.
16.	Schousboe JT, Kerlikowske K, Loh A, Cummings SR. Personalizing mammography by breast density and other risk factors for breast cancer: analysis of health benefits and cost-effectiveness. Annals of internal medicine. 2011;155(1):10-20.
17.	Vilaprinyo E, Forne C, Carles M, Sala M, Pla R, Castells X, et al. Cost-effectiveness and harm-benefit analyses of risk-based screening strategies for breast cancer. PloS one. 2014;9(2):e86858.
18.	Visvanathan K, Hurley P, Bantug E, Brown P, Col NF, Cuzick J, et al. Use of pharmacologic interventions for breast cancer risk reduction: American Society of Clinical Oncology clinical practice guideline. Journal of clinical oncology : official journal of the American Society of Clinical Oncology. 2013;31(23):2942-62.
19.	Moyer VA. Medications to decrease the risk for breast cancer in women: recommendations from the U.S. Preventive Services Task Force recommendation statement. Annals of internal medicine. 2013;159(10):698-708.
20.	Gail MH, Brinton LA, Byar DP, Corle DK, Green SB, Schairer C, et al. Projecting individualized probabilities of developing breast cancer for white females who are being examined annually. Journal of the National Cancer Institute. 1989;81(24):1879-86.
21.	Wang X, Huang Y, Li L, Dai H, Song F, Chen K. Assessment of performance of the Gail model for predicting breast cancer risk: a systematic review and meta-analysis with trial sequential analysis. Breast cancer research : BCR. 2018;20(1):18.
22.	Antoniou AC, Cunningham AP, Peto J, Evans DG, Lalloo F, Narod SA, et al. The BOADICEA model of genetic susceptibility to breast and ovarian cancers: updates and extensions. British Journal of Cancer. 2008;98(8):1457-66.
23.	Usher-Smith J, Emery J, Hamilton W, Griffin SJ, Walter FM. Risk prediction tools for cancer in primary care. British Journal of Cancer. 2015;113(12):1645-50.
24.	Gagnon J LE, The Clinical Advisory Committee on Breast Cancer Screening and Prevention, et al. Recommendations on breast cancer screening and prevention in the context of implementing risk stratification: impending changes to current policies. Current Oncology.2016;23(6)(e615-e625).
25.	Amir E, Evans DG, Shenton A, Lalloo F, Moran A, Boggis C, et al. Evaluation of breast cancer risk assessment packages in the family history evaluation and screening programme. Journal of medical genetics. 2003;40(11):807-14.
26.	Brentnall AR, Harkness EF, Astley SM, Donnelly LS, Stavrinos P, Sampson S, et al. Mammographic density adds accuracy to both the Tyrer-Cuzick and Gail breast cancer risk models in a prospective UK screening cohort. Breast cancer research : BCR. 2015;17(1):147.
27.	Meads C, Ahmed I, Riley RD. A systematic review of breast cancer incidence risk prediction models with meta-analysis of their performance. Breast cancer research and treatment. 2012;132(2):365-77.
28.	Tice JA, Cummings SR, Smith-Bindman R, Ichikawa L, Barlow WE, Kerlikowske K. Using clinical factors and mammographic breast density to estimate breast cancer risk: development and validation of a new predictive model. Annals of internal medicine. 2008;148(5):337-47.
29.	Obermeyer Z, Emanuel EJ. Predicting the Future - Big Data, Machine Learning, and Clinical Medicine. The New England journal of medicine. 2016;375(13):1216-9.
30.	Dreiseitl S, Ohno-Machado L. Logistic regression and artificial neural network classification models: a methodology review. Journal of biomedical informatics. 2002;35(5-6):352-9.
31.	Chen HC, Kodell RL, Cheng KF, Chen JJ. Assessment of performance of survival prediction models for cancer prognosis. BMC medical research methodology. 2012;12:102.
32.	Kourou K, Exarchos TP, Exarchos KP, Karamouzis MV, Fotiadis DI. Machine learning applications in cancer prognosis and prediction. Computational and structural biotechnology journal. 2015;13:8-17.
33.	Reinbolt RE, Sonis S, Timmers CD, Fernandez-Martinez JL, Cernea A, de Andres-Galiana EJ, et al. Genomic risk prediction of aromatase inhibitor-related arthralgia in patients with breast cancer using a novel machine-learning algorithm. Cancer medicine. 2018;7(1):240-53.
34.	Vanneschi L, Farinaccio A, Mauri G, Antoniotti M, Provero P, Giacobini M. A comparison of machine learning techniques for survival prediction in breast cancer. BioData mining. 2011;4:12.
35.	Heidari M, Khuzani AZ, Hollingsworth AB, Danala G, Mirniaharikandehei S, Qiu Y, et al. Prediction of breast cancer risk using a machine learning approach embedded with a locality preserving projection algorithm. Physics in medicine and biology. 2018;63(3):035020.
36.	Morrissey M. pedantics: Functions to Facilitate Power and Sensitivity Analyses for Genetic Studies of Natural Populations. 2018.
37.	Stef van Buuren [aut c, Karin Groothuis-Oudshoorn [aut], Alexander Robitzsch [ctb], Gerko Vink [ctb], Lisa Doove [ctb], Shahab Jolani [ctb], Rianne Schouten [ctb], Philipp Gaffert [ctb], Florian Meinfelder [ctb], Bernie Gray [ctb]. mice: Multivariate Imputation by Chained Equations. 2017.
38.	Katapodi MC, Northouse LL, Schafenacker AM, Duquette D, Duffy SA, Ronis DL, et al. Using a state cancer registry to recruit young breast cancer survivors and high-risk relatives: protocol of a randomized trial testing the efficacy of a targeted versus a tailored intervention to increase breast cancer screening. BMC cancer. 2013;13:97.
39.	Katapodi MC, Duquette D, Yang JJ, Mendelsohn-Victor K, Anderson B, Nikolaidis C, et al. Recruiting families at risk for hereditary breast and ovarian cancer from a statewide cancer registry: a methodological study. Cancer causes & control : CCC. 2017;28(3):191-201.
40.	Progeny. Family data and pedigree information was stored and manipulated using the genetic data management system (Progeny CLINICAL Version N) from Progeny Software (Progeny Software LLC, Delray Beach, FL, www.progenygenetics.com).
41.	Team RC. R: A Language and Environment for Statistical Computing. R Foundation for Statistical Computing; 2017.
42.	Zhang F. Breast Cancer Risk Assessment. 2.0 ed2018.
43.	Dinov ID. Data Science and Predictive Analytics: Biomedical and Health Applications Using R: Springer; 2018.
44.	Murdoch TB, Detsky AS. The inevitable application of big data to health care. JAMA. 2013;309(13):1351-2.
45.	Toga AW, Dinov ID. Sharing big biomedical data. Journal of big data. 2015;2(1):7.
46.	Dinov ID, Heavner B, Tang M, Glusman G, Chard K, Darcy M, et al. Predictive big data analytics: a study of Parkinson’s disease using large, complex, heterogeneous, incongruent, multi-source and incomplete observations. PloS one. 2016;11(8):e0157077.
47.	Andrea Dal Pozzolo OCaGB. unbalanced: Racing for Unbalanced Methods Selection. 2015.
48.	Chawla N, Bowyer K, Hall L, Kegelmeyer W: SMOTE: synthetic minority over-sampling technique. J Art Intell Res. 2002, 16: 321-357.
49.	Kohavi R, editor A study of cross-validation and bootstrap for accuracy estimation and model selection. International Joint Conference on Artificial Intelligence; 1995: Montreal, Canada.
50.	Ng AY. Preventing "Overfitting" of Cross-Validation Data.  Proceedings of the Fourteenth International Conference on Machine Learning. 657119: Morgan Kaufmann Publishers Inc.; 1997. p. 245-53.
51.	Strimme K. Package ‘crossval’. 2015. p. Contains generic functions for performing cross validation and for computing diagnostic errors.
52.	Hickey KT, Katapodi MC, Coleman B, Reuter‐Rice K, Starkweather AR. Improving Utilization of the Family History in the Electronic Health Record. Journal of Nursing Scholarship. 2017;49(1):80-6.
