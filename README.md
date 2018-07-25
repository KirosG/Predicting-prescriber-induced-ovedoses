===============================================================================

## Predicting prescriber induced overdoses

---

**Author : Kiros Gebremariam**
---

---

Cohorts of the Data Science Immersive, General Assembly @ Washington DC campus
---

---

=================================================================================

---

### DATA SCIENCE IMMERSIVE FINAL CAPSTONE

--------------------------------------------------------------------------
===

# Predicting prescriber induced overdoses using machine learning

**Introduction**

For my capstone project while taking the data science immersive program at General Assembly, I’ve decided to tackle the major public health issue that is the opioid crisis in the united states of America.

The objective of this capestone is to **identify types of prescribers that are a high-risk for opioid related fatalities across the country and predict most influential opioids leading to opiod related deaths.**

![](https://cdn-images-1.medium.com/max/800/1*FdlXyQW_2hzrwwRoxhUbTQ.png)

[History of opioids](https://docs.google.com/presentation/d/1FiI4FG7PvAWse-es0xpTgp3MQs4dGWJPBNqCEQtqqik/edit#slide=id.g3d926e07e2_1_349)

![](https://cdn-images-1.medium.com/max/800/1*WZa4WXDyovPkCPKOCkvjhw.png)

[How opioids become catastrophe](https://docs.google.com/presentation/d/1FiI4FG7PvAWse-es0xpTgp3MQs4dGWJPBNqCEQtqqik/edit#slide=id.g3d926e07e2_1_349)

Right now, our country faces an average of 115 opioid overdose deaths each day according to the data from wonder/CDC. Over[280 million prescriptions were written in 201](https://www.cdc.gov/drugoverdose/data/overdose.html)2 alone and are a big contributing factor to this issue. Prescription opioid abuse, misuse, and dependence as a public health hazard is a daily phenomenon now; according to Centers for Disease Control and Prevention (CDC) , over[1,000 people are treated in emergency department](https://www.cdc.gov/drugoverdose/data/overdose.html)everyday for misusing prescription opioid drugs. The number of overdose deaths from substance abuse in the US increased from around 9,000 in 1990 to more than 64,000 in 2016, up by 23% increase from the previous year. According to the data source 75% of drug OD deaths involve opioids (prescribed or illegal). Prescription opiate drugs, especially methadone, oxycontin, and hydrocodone, are believed to have played a significant role in this public health crisis sweeping the US. In addition to the health issues arising from overdose, opioid epidemic requires significant economic resources from cities and state governments for emergency call response and policing. The estimated total costs of[US opioid epidemic reaches](https://www.ncbi.nlm.nih.gov/pubmed/27623005)over 78 billion dollars.

![](https://cdn-images-1.medium.com/max/800/0*1z8RJc8205PI5wJH)

Opioids: Addictive painkillers

The major source of diverted[opioids is physician prescription](https://www.sciencedirect.com/science/article/pii/S0091743515001036). However, opioids prescription to patients with acute pain and patients with chronic pain requires a careful distinction. As Opioid is regarded as one of the most effective drugs for the acute pain management, limiting its use for patients who are in urgent need of pain control, post surgical status, cancer patients, and other health crisis, would not only be inhumane but also defeat its intended purpose. On the other hand, use of opioids for chronic non-malignant pain control has remained[controversial for decades](https://pdfs.semanticscholar.org/218d/30e5581e51584e2cdfde0cb12ab67fd2a557.pdf)and requires closer look in regards to the current opioids health crisis.

![](https://cdn-images-1.medium.com/max/800/1*hMHtyGwijhI2EhlFZl8ZOg.png)

[The severity of chronic pain as compared to Coronary artery disease(CAD)](https://docs.google.com/presentation/d/1FiI4FG7PvAWse-es0xpTgp3MQs4dGWJPBNqCEQtqqik/edit#slide=id.g3d926e07e2_1_349)

Asdata scientists, we can’t really question whether doctors are pushing prescriptions from sponsorship from pharmaceutical companies, or if they are constantly barraged by patients claiming they are in severe pain and actually need the medication, or really, most other factors for that matter. So, what I wanted to do was try and find the likelihood that a provider would prescribe an opioid and identify any patterns, if any, from that data. Based on my personal research from the currently published materials by CDC and the National institute of health the number one[cause of death from age 15–50 years](https://docs.google.com/presentation/d/1FiI4FG7PvAWse-es0xpTgp3MQs4dGWJPBNqCEQtqqik/edit#slide=id.g3d926e07e2_1_349)in the US is drug opioids death. i have show the comparison with other significant events from our history as follows:-

- Drug OD deaths in 2016: 64,000
- Vietnam total deaths (1965–1975) 58,000
- Motor vehicle Accident deaths in 2016 40,000
- HIV deaths in peak year (1995) 47,000
- Gun deaths in peak year (1993) 39,000

This study attempts to build a predictive model of likelihood of a healthcare provider prescribing opioids drugs to patients with chronic pain. More specifically, we will identify correlated features of non-opioid drugs prescription history with opioid prescription. In addition, we will distinguish gender, specialty, and location that are more highly correlated to the prolonged use of a long term (more than 12 weeks) supply of opioids.

**Datasets and Inputs**

Atotal of eight datasets, detailed data, provider summary, national drug summary table, national health expenditure(NHE), property and violent crime by state, mental health deaths, and state drug summary table , were obtained from the web page of the Centers for Medicare and Medicaid Services (CMS),kaiser Family Foundation (KFF), CDC/wonder as well as Department of Justice . The detailed data contains 5 the information on prescription drugs prescribed by individual health care providers and paid for under the Medicare Part D Prescription Drug Program in year of 2016. It includes the detailed prescription information such as the brand drug name, the number of patients who filled the drug more than ten times, the aggregate number of day’s supply for which the prescription drug was dispensed.

![](https://cdn-images-1.medium.com/max/800/0*Gr4pa5bQkr90mIM5)

Prescriber’s information

The dataset provider summary table contains the demographics of the individual prescribers (n=1,131,550). Briefly, it includes the National provider identification(NPI) number, name, gender, address, medical credential, specialty, and medicare enrolment status. It also includes the summary of the abstracted clinical data such as the number of total claims count from the prescriber, total opioid claim count based on the supply of all prescription drugs, total claims of antibiotic drugs, total claims of high-risk medication (HRM) drugs, total claims of antipsychotic drugs, and more importantly, the number of patients treated with opioid prescriptions, and the ratio of opioid prescription to non-opioid prescription.

The rest two datasets are national drug summary table and state drug summary table. It lists the prescription drug names, whether the drug is categorised as antibiotics (n=78), opioids (n=29), antipsychotic (n=28), HRM (n=68), or others (n=951) and the number of prescribers of that drug grouped by nation and state, respectively. For more detailed information on how the dataset were collected, please refer to the CMS’s webpage[here](https://www.cms.gov/About-CMS/About-CMS.html). The other data sets the NHE shows the percentage share of the prescription drugs all inclusive from the national health budget and the data set includes from 1960–2016. The KFF dataset includes all the mental health deaths by state that have some level of connection with opioids. The crime data set was collected from multiple sources and agencies using the query method in order to see crimes linked to the opioids or not and shows by state, either it happened in urban area or rural areas of the country.

The box plot was chosen to show the top prescriber-specialists of the opioid drugs abused on the professional category and it turns out that the cardiology (`diseases and abnormalities of the heart.`) specialists have the highest variability, followed by Endocrinology(`the branch of physiology and medicine concerned with endocrine glands and hormones`),psychiatry(`the study and treatment of mental illness, emotional disturbance, and abnormal behavior.`), Nephrology(`the branch of medicine that deals with the physiology and diseases of the kidneys.`) and pulmonarydisease(`chronic obstructive pulmonary disease. : pulmonary disease (such as emphysema or chronic bronchitis) that is characterised by chronic typically irreversible airway obstruction resulting in a slowed rate of exhalation —abbreviation COPD`).

**My Solution Statement**

I start by merging two datasets, detailed data and[provider summary](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/PartD2016.html), to get combined features of providers’ personal information and prescription history of drugs (sorted by its generic names, n=1154). Two new attributes, op_avg_supply and op_longer , are added. Op_avg_supply is the aggregate number of days supply divided by total of patients for which opioids drugs were dispensed. Op_longer is labeled 1 if the provider has Op_avg_supply greater than 84 days (12 weeks), and 0 if less than 84 days. Then i train supervised classification models according to the op_longer labels to solve this large scale nonlinear problem. This projects will consists of three parts: exploratory data analysis, train/test split, building pipeline to finetune models via Scikit learn, and extension to the neural networks in TensorFlow.

As the detailed data contains more than 25 million instances and its volume is larger than 3.2 GB, it easily takes up the memory of local machine, especially when we combine it with prescriber summary dataset to make a wide table. As such, we will utilize’s pandas’ TextFileReader module and read in the instances by small chunks (size=100,000). In order to make sure of seamless and reproducible inputs, i automate the data input pipeline via data cleaning, feature selection, and feature scaling.

Exploratory data analysis In order to gain insights, i explore the data by visualising each attribute on some randomly selected features as shown below. Lets see the visuals of the data sets as follows

According to the datasets the number of opioid prescriptions dispensed by doctors steadily increased from 112 million prescriptions in 1992 to a peak of 282 million in 2012, since 2012 declined to 236 million in 2016. In 2016, 6.2 billion hydrocodone pills were distributed nationwide . In 2016, according to the CDC around 5 billion Oxycodone (ox i koe’ done) tablets were distributed in the United States, which makes Oxycodone (percocet) the second most prevalent opioid. Based on these i come to the point that it the vicious circle problem, in our country that we are 5% of the worlds population but 80% of the worlds opioids are prescribed here and its easy to see the severity of over prescription of opiates.Based on the dataset the state of California is leading with the highest number of deaths due to overdose. Kentucky has been hit particularly hard with 1,419 reported overdose deaths in 2016, which is 33.5 per 100,000 people according to the CDC wonder data and of those deaths 989 which is 23.6 per 100,000 people involved some type of opioids. it was followed by WestVirginia ,which is 884 reported overdose deaths (52 deaths per 100,000 people).

![](https://cdn-images-1.medium.com/max/800/1*hjUj193KCA7MYIS8bDd6dQ.png)

Opioid related deaths count by state

![](https://cdn-images-1.medium.com/max/800/1*iXfK9xfBRqRr_iZcvptDHA.png)

[state and Speciality by the top 11 opioids](https://public.tableau.com/profile/kirosdsi.com#!/vizhome/CapstoneUSAOpiodscrisisByStateandSpeciality2018/ByStateAndSpecialty)

![](https://cdn-images-1.medium.com/max/800/1*dg0NYRHxaU5ufAfiNyuJmg.png)

opioids prescription rate versus the extended release rate by state

![](https://cdn-images-1.medium.com/max/800/1*NJt_-Fw7aBS4tQfiQE054g.png)

[interactive visualisation of speciality variability per opioid prescription](https://plot.ly/~kiros/126)

![](https://cdn-images-1.medium.com/max/800/1*AeBTGH2cVQxs-uDlktQ_hw.png)

Speciality variability of prescribing opioids

![](https://cdn-images-1.medium.com/max/800/1*XRQhrUWPgqmb40UrN8tb0g.png)

state visuals: as the thickness of the colour enhances the death amount increases due to opiods

what do i learn from the datasets comparing states and understanding the above opioid prescription rate and the extended release rate. I will sumarise in the following sentence. Opioids bind to receptors in the brain and spinal cord which in turn disrupt the pain signal by activating the reward areas of the brain so that the dopamine hormone to be released and to create the feeling of euphoria, which means being high or happy. The golden standard for any pain medication is morphine and others are converted to morphine milligram equivalent(MME) and we all know morphine and codeine are naturally derived from opium poppy plan more commonly grown in Asia, central and southern America. The illegal drugs according to CDC like heroin are synthesised from morphine. on the other hand,Hydrocodone and Oxycodone are semi-synthetic opioids manufactured in laboratories with natural synthetic ingredients. According to the dataset and above graph between 2007 and 2016, the most widely prescribed opioid almost by all specialities and across all the 50 states was hydrocodone(Vicodin).please see the above graph[state and Speciality by the top 11 opioids](https://public.tableau.com/profile/kirosdsi.com#!/vizhome/CapstoneUSAOpiodscrisisByStateandSpeciality2018/ByStateAndSpecialty)in my public tableau account using the link to see the interactive graph. methadone is another fully synthetic opioid, which is dispensed for patients recovering from heroin addiction to help them relieve the symptoms of withdrawal. opioid use disorder is one of the clinical terminologies used in the medical practice referring for opioid addiction or abuse. its generally, known that people who become dependent on any of these pain killers or opioids may experience withdrawal symptoms when they start to stop taking the pills. For any person who worked or practiced in any medical practice, its clear that dependence is often coupled with tolerance , meaning that opioid users need to take increasingly larger doses of the medication for the same effect. The economic terminology for such effect is called marginal utility. What it means is that the additional satisfaction or euphoria an opioid user gets from consuming one more unit of a pill. According to[Substance Abuse and Mental Health Services Administration](https://www.samhsa.gov/data/sites/default/files/NSDUH-FFR1-2016/NSDUH-FFR1-2016.pdf)about 11.5 Million American’s age 12 and older misused prescription pain medications in 2016 and around 948,000 or 0.3 % of the united states population age 12 and above used heroin in 2016. Its very significant number and needs more strategic planning and action pints, i guess that’s why the Trump[Administration on February 9,2018 allocated around 6 billion dollars for opioid program , with $ 3 billion allocated for 2018 and $ 3billion allocated for 2019 to tackle the epidemics.](https://energycommerce.house.gov/news/press-release/walden-passage-bipartisan-budget-act-2018/)

**Methods**

The baseline of the data set to overcome is 53.7%. The problem with machine learning is that building an effective model can require a ton of human input. While working my capstone time was so demanding as i was so engaged working the Washington, DC crime prediction and the data cleaning took’s almost my entire time. I never took it seriously that most data scientists spent 80% of their time cleaning and wrangling the data. Humans have to figure out the right way to transform the data before feeding it to the machine learning model. Then they have to pick the right machine learning model that will learn from the data best, and then there’s a whole bunch of model parameters to tweak that can make the difference between a dud and a Nostradamus-like model. Building these pipelines — i.e., sequences of steps that turn the raw data into a predictive model — can easily take weeks of tinkering depending on the difficulty of the problem. This is obviously a huge issue when machine learning is supposed to allow machines to learn on their own. When almost all my developed models, some of them they work better on the training data and underperformed on test data i used the[Tree-based Pipeline Optimisation Tool (TPOT)](https://github.com/rhiever/tpot) . TPOT is a Python tool that automatically creates and optimises machine learning pipelines using[genetic programming](https://en.wikipedia.org/wiki/Genetic_programming). Think of TPOT as your “Data Science Assistant”: TPOT will automate the most tedious part of machine learning by intelligently exploring thousands of possible pipelines, then recommending the pipelines that work best for your data.

![](https://cdn-images-1.medium.com/max/800/1*yc5A3nvnQjC8k7HGdsXFxg.png)

Machine learning pipeline, and what parts of the pipeline TPOT automates.

Then, based onTPOT recommends me to use decision tree classifier and when i run my model i end up getting 89% on the test data and 99.8% on my training data set which is different from the TPOT recommendation and after tuning for hyperperameters

![](https://cdn-images-1.medium.com/max/800/1*5p6x5u-8wQ64dO7lQ7dLaA.png)

DTC

Then i tried other classifiers like random forest Classifier, Logistic Regression,Decision tree, Adaboost classifier and Neural Network using Keras). Finally i chose to apply Neural networks and performed better than the TPOT recommended optimiser. The neural network uses Gender, speciality as my target variable was binary classification problem, opiod prescriber or not opioid prescriber (0 to 1). The model trained on 21813 samples, tested on 2424 samples. The neural network model has the number of inputs which i used 354 features as hidden layers with relu activation function. The output layer uses sigmoid since it is a classification problem. The model compiler uses binary cross-entropy as a loss function, Adam optimiser, and accuracy metrics with an early stop to avoid exhaustive training. The accuracy score of the model was 91.4% with 21.7% loss.

![](https://cdn-images-1.medium.com/max/800/1*WZQzSraSr8TjZVSYxmJt9g.png)

![](https://cdn-images-1.medium.com/max/800/1*1yMZVR2RueHXiDg0ZyjhVQ.png)

![](https://cdn-images-1.medium.com/max/800/1*JF0dYAiUtWTtU1vcYJgGLw.png)

![](https://cdn-images-1.medium.com/max/800/1*hDo2b_4OJrXJJr9Dflm-QQ.png)

Model accuracy score and loss for NN

Many features came up for all the models. Cariso- prodol, diazepam, alprazolam, gabapentin, pregabalin, hydroxychloroquine sulfate, cyclobenzaprine HCl, and tizanidine HCl were highly associated with the label based on all the model. As we expected from the EDA section , of medical specialties, pain management, interventional pain management, rheumatology, hematology, cardiology and family practice and hospice and palliative care were estimated that the label is true with higher probability.

A limitation of the study is that the dataset only includes a snapshot of the total population as beneficiaries of Medicare are elderly population of age greater than 65. The original materials can be accessed[here](https://github.com/KirosG/Predicting-prescriber-induced-ovedoses)

*This article is a living and breathing matter. Your feedback matters to me. Please leave comments on what resources I should add and what you found the most helpful when you were learning machine learning. Thanks a lot for reading!*



























  Additional 

## Introduction:

---

This capestone was initaited with an idea that why are so much more physicians presecribing medications that can lead to overdose. I have worked with patients for more than a year in a clinic as well as a hospital and saw significant amount of patients requesting pain relief medications again and again. I have seen people i know been affected with the chronic and life threatening overdose. This capstone is a supervised training that uses RandomForest Classifier, Logistic Regression, and Neural Networks by using Keras to predict prescriber induced Overdose using datasets from CDC/Winder,CMS and the department of justice. The opiod prescriber is used as a target variable. 

---

The objective of this capestone is to **identify types of prescribers that are a high-risk for opioid related fatalities across the country and predict most influential opioids leading to opiod related deaths.**

---

### Data Cleaning:

 The dataset for this capstone was collected from CDC,CMS,KAISER FAMILY FOUNDATION. The public health data was extracted from [CDC](https://wonder.cdc.gov/) which is and metadata from 2011 - July 2016. Downloading data from wonder requires the signing f online conscent and querring the needed information separately and the system will generate the text versions and i have extracting individually for the text versions the deaths associated with opiods. I noticed some anomalies when extracting data from Wonder in large due to the system or functionality of wonder tool they have to group the needed data based on the querry.  The opiods related with Drug enforcement Agency (DEA) licensed specialities connected with the opiods were downloaded from FDA and cross matched with the 2013-2016 Opiods drusglist for the year 2013-2016 can also be accessed [here](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html). The Part D Prescriber PUF file was sas version and in texti downloaded into individual tab separated text files as dowloading the 3.2GB data at once and extracting needs significant processing power besides I noticed some anomalies when extracting data from Wonder in large due to the system or functionality of wonder tool they have to group the needed data. The otherData was extraced from CMS Medicare [Part D Opioid Prescriber Data]( https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/Part-D-Prescriber.html),[cms](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html) and  [NHE](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NationalHealthAccountsStateHealthAccountsProvider.html). All the datasets were collected from different sources and validated. Somedatasets are official querried from respective government institutions using private usercode and adjusted to the subject after cleaning. The overall dataset set was cleaned by dropping the unnecessary columns and missing data since the total missing data was very small compared to an overall dataset. In addition, feature engineering was performed by converting the helpful column into a binary classification, opiod prescriber and not opiod prescriber in one column as 1 or 0.

### Exploratory Data Analysis

In overll, the opiod prescribing behaviour of health professionals were exponentially increased since opiod epidemic begin in the USA in 1996.The start of the Epidemic according the literatures and the CDC is the FDA approval of the Purdue Pharmaceuticals drugs and OxyContin for non-cancer pain, which caused  the beginning of the epidemics, though purdue pleaded guilty in 2007 and accepted a fine of $635 million fine. Grouping the specialists by the number of prescriptions they give to patients a significant amont of deaths across almost all states were observed. According to the datasets the number of opioid prescriptions dispensed by doctors steadily increased from 112 million prescriptions in 1992 to a peak of 282 million in 2012, since  2012 declined, falling to 236 million in 2016. In 2016, 6.2 billion hydrocodone pills were distributed nationwide. The second most prevalent opioid was oxycodone (Percocet). In 2016, according to the CDC around  5 billion oxycodone tablets were distributed in the United States, which i say it the bells curve,USA is 5% of he worlds population but 80% of the worlds opiods are prescribed here and its easy to see the severity of over prescription of opiates.Based on the dataset the state of california is leading with the highest numebr of deaths due to overdose. Kentucky has been hit particularly hard with 1,419 reported overdose deaths in 2016, which is 33.5 per 100,000 people according to the CDC wonder data and of those deaths 989 which is 23.6 per 100,000 people involved some type of opiods. it was followed by westverginia which is 884 reported  overdose deaths which is 52 per 100,000 people. The dataset has more than 25,000 prescribers after the initial clean up and prescriber shows that there are 108 unique Specialities, and 63 of them have a length of less than 40, so adjusting those so they can be a bit more balanced and sorted into specific specialities as others and specialities. The full analysis of the data sets and features are presented in notebook 1.2 & 1.3. 

---

# Prepare the Data for Modeling and feature importance visual

---

## Feature Selection

---

Now we have  more than 355 features but what does they mean or actually how much do we need to know about these features. my Answer to this question would be  not need to know meaning of all the 355 features. What's important is that during the Exploratry data analysis  when we use the `.describe()` for numerical values and the `.describe(include['objects])`, which describes all objects' we already have some insights to imagine in our mind we should know something like variance, standart deviation, number of sample (count) or max, min values. These type of information helps to understand about what is going on  with the data.  Therfore, standirdization or normalization are important when  before visualization, feature selection, feature extraction or classificaiton. In order to visualizate  the data  in python, its always good to have the jupyter notbook inputs or libraries or packages installed like matplotlib or seaborn or plotly. The plots i used in this capstone are dominantly bar plots, histograms and to some extent maps. The visulization is one of the best methods to understand the data and helps in selecting what features to use for modeling and further extraction or elimination. 

There are mutiple ways that any datascientist would use to select features from the dataset.The methods can range from  feature selection with correlation either using heatmaps or just correlation, univariate feature selection, recursive feature elimination (RFE), recursive feature elimination with cross validation (RFECV) and tree based feature selection. Here i used correlation feature selection. Since my dataset has more than 355 features, most of them drug names. I will select specific features for model training. The original dataset contains 355 features, most of which are categorical attributes, dominantly the list of drug names that are approved as pain medications; that need special AED licensed prescriber.Here,my main target is to predict the overdoses using the  the list of prescriber specialists with NPI information and the FDA approved drug lists. The data set has only total opiod cliams and total claim counts and i took the standard prescription for opiod drugs is 84 days which is 12 weeks. The standards  used to measure the opiod overdose use morphine as gold standard. other drug types of drugs depending on their strength are measured  using morphine milligram equivalents (MME). according to the study by [CDC](https://www.cdc.gov/mmwr/volumes/66/wr/mm6626a4.htm?s_cid=mm6626a4_w) high-dose prescribing rates are classified as prescriptions with daily dosage greater than or equal to 90.  Therefore, based on the evidences i got from CDC and KFF i created an additional feature in the data cleaning, pre processing that shows avg_op_supply which i limit to the standard to be 84 days and any ones who prescribes the category of medications under the controlled substance act(CSA). The CSA is used for organizing drugs based on the risk of abuse or harm to users in five and my capestone focuses on the approved by [FDA](https://www.fda.gov/drugs/drugsafety/informationbydrugclass/ucm251735.htm) and [DEA](https://www.deadiversion.usdoj.gov/schedules/) to be prescribed by licensed and certified health professional.  These drug lists that are considered controlled substances under the Controlled Substances Act (CSA) are divided into five schedules.  An updated and complete list of the schedules is published annually in [Title 21 Code of Federal Regulations (C.F.R.) §§ 1308.11 through 1308.15](https://www.deadiversion.usdoj.gov/21cfr/cfr/2108cfrt.htm).

Therefore, for analysis and visualization  i only took those physicians who have greater opiod cliams from the center for medical services dataset and created a feature average opiod supply  by dividing the total cliamcount by the total opiod cliam count and reviewed those specialists who prescribe more than the set limit of 12 weeks. The opiod longer feature was created as a new feature that measures the length of opiod prescription supply more than 84 days. As been visualized in notebook 1.3, significant amount of prescribers are family physicians, followed by internal medicine,nurse practitioners, Physicain Assistant and physical medicine and rehabilitation. When i group based on speciality and the vsuals can be accessed   [here top 20](https://plot.ly/~kiros/112),[here state and drug tableau](https://public.tableau.com/profile/kirosdsi.com#!/vizhome/CapstoneUSAOpiodscrisisByStateandSpeciality2018/ByState) and the lists are as follows:-

> $'Cardiology', 'Nephrology', 'Endocrinology', 'Neurology'  'General Practice', 'Internal Medicine', 'Urology'$,  
> $'Pulmonary Disease', 'Gastroenterology', 'Family Practice', 'Infectious Disease','Psychiatry'$ 
> $'Nurse Practitioner', 'Ophthalmology','Allergy/Immunology', 'Otolaryngology', 'Psychiatry & Neurology'$ , $'Rheumatology', 'Dermatology', 'Obstetrics/Gynecology'$

---

### Models

---

The baseline  of the data set to overcome is 53.7%. Out of all the models (RandomForest Classification, Logistic Regression,Decision tree,Adaboost classifier, TPOTClassifier  and Neural Network using Keras), the Descision tree,random forest neural network out performed baseline and other models with 91% accuracy score on the test dataset with loss of 23%. The neural network uses Gender, speciality  as my target variable was binary classification problem, opiod prescriber or not opiod prescriber (0 to 1). The model trained on 21813 samples, validate on 2424 samples. The neural network model has the number of inputs as  hidden layers with relu activation function. The output layer uses sigmoid since it is a classification problem. The model compiler uses binary cross-entropy as a loss function, Adam optimizer, and accuracy metrics with an early stop to avoid exhaustive training. I have also used TPOT to see which model has best features and estimators and does not perform much better. The models i run to predict the opiod prescribers usinig binary method can be accesed in  notebooks 1.4 to 1.6.

---

### Conclusion

---

The opiod epidemic is increasing at alaring rate. Drug overdoses account for a significant portion of accidental deaths in adolescents and young adults in the country, which are tomorrow leaders of the nation. The majority of drug overdoses  according to the dataset cross validated from multple sources indicate they involve opioids, a class of inhibitor molecules that disrupt transmission of pain signals through the nervous system. Medically, they are used as powerful pain relievers; however, they also produce feelings of euphoria, which is temporary happiness.. This temporary happiness and avoidance of pain makes the individual to consume more doses than prescribed at the end its highly addictive and prone to abuse. The use of opiods to mitigate or reduce chronic pain is one of the hot and controversial topics nowadays.There is no good studies show long term improved pain scores with chronic opioids rather than the ultimate death of the productive society and care must be taken. The prescription of opiods for only severe pain that sustain more than three months and no other drug mitigates, trying alternative non addictive medications is important, if there is any one taking medication, stoping would be appropriate. The interesting point from multiple sources and KFF datasets indicate most people who are addicted or overdesed and visited the emergency room got the medication from friends or from strangers , which indicates the prescription drugs quantity prescribed should not be more than the recommended and ther msu also exst a mechanism to remove left over pills like  either returning to the facility so that they will be removed with the hazardous wastes or submitting to the local police.

[presentation](https://docs.google.com/presentation/d/1FiI4FG7PvAWse-es0xpTgp3MQs4dGWJPBNqCEQtqqik/edit#slide=id.g3e1de2c206_0_7)

==================================================================================

### Datasources

---

- CDC  : 
   -[Current Multiple cause of Death](https://wonder.cdc.gov/mcd-icd10.html)
   -[Multiple Cause of Death Data|NCHS](https://wonder.cdc.gov/wonder/help/mcd.html)
   -[National Center for Health Statistics](https://www.cdc.gov/nchs/index.htm)
   -[KFF smha-expenditures-per-capita](https://www.kff.org/other/state-indicator/smha-expenditures-per-capita/?currentTimeframe=0&selectedRows=%7B%22wrapups%22:%7B%22united-states%22:%7B%7D%7D%7D&sortModel=%7B%22colId%22:%22Location%22,%22sort%22:%22asc%22%7D)
   -[Vital Signs: Changes in Opioid Prescribing in the United States, 2006–2015](https://www.cdc.gov/mmwr/volumes/66/wr/mm6626a4.htm?s_cid=mm6626a4_w)
   -[List of Drugs](ftp://ftp.cdc.gov/pub/Health_Statistics/NCHS/Publications/NVSR/65_09/Table01.xlsx)

  -CMS: [NationalHealthAccountsStateHealthAccountsProvider](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NationalHealthAccountsStateHealthAccountsProvider.html),[NationalHealthExpendData](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/downloads/dsm-16.pdf)

- Medicare Provider Utilization and Payment Data: [Part D Prescriber Data CY 2013-2016](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/Part-D-Prescriber.html)

  - Part [D Prescriber Data CY 2016](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/PartD2016.html)

  - National Opioid Epidemic based on morphine mg equivalents[mme](http://opioid.amfar.org/indicator/mme_percap) 

  - Medicare Part D [Prescriber Look-up]( https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html)

### Technical terminologies and definitions can be accessed from the following address

---

   [Prescription _opioids](https://www.drugabuse.gov/publications/drugfacts/prescription-opioids)

   [SCHEDULES OF CONTROLLED SUBSTANCES](https://www.deadiversion.usdoj.gov/21cfr/cfr/2108cfrt.htm)

---

#### Data Dictionary :

=================================================================================
|Term                           |  Definition

|Opioids                        | are a class of drugs naturally found in the opium poppy plan

|common prescription opioids    | hydrocodone (Vicodin®) oxycodone (OxyContin®, Percocet®). oxymorphone (Opana®),morphine (Kadian®,Avinza®)
                                | codeine and fentanyl

|NPI                            | unique National Provider Identifier number

|Gender                         | (M/F)

|State                          | U.S. State by abbreviation

|Credentials                    | set of initials indicative of medical degree

|Specialty                      | description of type of medicinal practice

|Opioid.Prescriber              |  boolean label indicating whether or not that individual prescribed opiate drugs more than 10 times in the year 

#### Tableau Visualization

---

- [State and speciality based visuals](https://public.tableau.com/profile/kirosdsi.com#!/vizhome/CapstoneUSAOpiodscrisisByStateandSpeciality2018/ByState)

### Adverse effects of prescrption Drugs

 =================================================================================

- [impact of prescription](https://www.drugfreeworld.org/drugfacts/prescription-drugs.html)
  - 
### Part D Prescriber- Opioids List of Drugs

A long list of drugs with numeric values indicating the total number of prescriptions written for the year by that 
individual

---

|Drug Name                              | Generic Name

---

|ABSTRAL                                  |FENTANYL CITRATE
|ACETAMINOPHEN-CODEINE                    | CETAMINOPHEN WITH CODEINE
| ACTIQ                                   | FENTANYL CITRATE
| ASA-BUTALB-CAFFEINE-CODEINE             | CODEINE/BUTALBITAL/ASA/CAFFEIN
| ASCOMP WITH CODEINE                     | CODEINE/BUTALBITAL/ASA/CAFFEIN
| ASPIRIN-CAFFEINE-DIHYDROCODEIN          | ASPIRIN/CAFFEIN/DIHYDROCODEINE
| AVINZA                                  | MORPHINE SULFATE
|  BELBUCA                                | BUPRENORPHINE HCL
| BELLADONNA-OPIUM                        | OPIUM/BELLADONNA ALKALOIDS
| BUPRENORPHINE HCL                       | BUPRENORPHINE HCL
| BUTALB-ACETAMINOPH-CAFF-CODEIN          | BUTALBIT/ACETAMIN/CAFF/CODEINE
| BUTALB-CAFF-ACETAMINOPH-CODEIN          | BUTALBIT/ACETAMIN/CAFF/CODEINE
| BUTALBITAL COMPOUND-CODEINE             | CODEINE/BUTALBITAL/ASA/CAFFEIN
| BUTORPHANOL TARTRATE                    | BUTORPHANOL TARTRATE
| BUTRANS                                 | BUPRENORPHINE
| CAPITAL W-CODEINE                       | ACETAMINOPHEN WITH CODEINE
| CARISOPRODOL COMPOUND-CODEINE           | CARISOPRODOL/ASPIRIN/CODEINE
|CARISOPRODOL-ASPIRIN-CODEINE             | CARISOPRODOL/ASPIRIN/CODEINE
| CODEINE SULFATE                         | CODEINE SULFATE
| CONZIP                                  | TRAMADOL HCL
| DEMEROL                                 | MEPERIDINE HCL
| DIHYDROCODEIN-ACETAMINOPH-CAFF          | ACETAMINOPHEN/CAFF/DIHYDROCOD
| DILAUDID                                | HYDROMORPHONE HCL
| DISKETS                                 | METHADONE HCL
| DOLOPHINE HCL                           | METHADONE HCL
| DURAGESIC                               | FENTANYL
| EMBEDA                                  | MORPHINE SULFATE/NALTREXONE
| ENDOCET                                 | OXYCODONE HCL/ACETAMINOPHEN
| EXALGO                                  | HYDROMORPHONE HCL
| FENTANYL                                | FENTANYL
| FENTANYL CITRATE                        | FENTANYL CITRATE
| FENTORA                                 | FENTANYL CITRATE
| FIORICET WITH CODEINE                   | BUTALBIT/ACETAMIN/CAFF/CODEINE
| FIORINAL WITH CODEINE                   | CODEINE/BUTALBITAL/ASA/CAFFEIN
| HYCET                                   | HYDROCODONE/ACETAMINOPHEN
|HYDROCODONE-ACETAMINOPHEN                | HYDROCODONE/ACETAMINOPHEN
| HYDROCODONE-IBUPROFEN                   | HYDROCODONE/IBUPROFEN
| HYDROMORPHONE ER                        | HYDROMORPHONE HCL
| HYDROMORPHONE HCL                       | HYDROMORPHONE HCL
| HYSINGLA ER                             | HYDROCODONE BITARTRATE
| IBUDONE                                 | HYDROCODONE/IBUPROFEN
| KADIAN                                  | MORPHINE SULFATE
| LAZANDA                                 | FENTANYL CITRATE
| LEVORPHANOL TARTRATE                    | LEVORPHANOL TARTRATE
| LORCET                                  | HYDROCODONE/ACETAMINOPHEN
| LORCET HD                               | HYDROCODONE/ACETAMINOPHEN
| LORCET PLUS                             | HYDROCODONE/ACETAMINOPHEN
| LORTAB                                  | HYDROCODONE/ACETAMINOPHEN
| MEPERIDINE HCL                          | MEPERIDINE HCL
| METHADONE HC                            | METHADONE HCL
| METHADONE INTENSOL                      | METHADONE HCL
| METHADOSE                               | METHADONE HCL
| MORPHINE SULFATE                        | MORPHINE SULFATE
| MORPHINE SULFATE ER                     | MORPHINE SULFATE
| MS CONTIN                               | MORPHINE SULFATE
| NORCO                                   | HYDROCODONE/ACETAMINOPHEN
| NUCYNTA                                 | TAPENTADOL HCL
| NUCYNTA ER                              | TAPENTADOL HCL
| OPANA                                   | OXYMORPHONE HCL
| OPANA ER                                | OXYMORPHONE HCL
| OPIUM TINCTURE                          | OPIUM TINCTURE
| OXYCODONE HCL                           | OXYCODONE HCL
| OXYCODONE HCL ER                        | OXYCODONE HCL
| OXYCODONE HCL-ASPIRIN                   | OXYCODONE HCL/ASPIRIN
| OXYCODONE HCL-IBUPROFEN                 | IBUPROFEN/OXYCODONE HCL
| OXYCODONE-ACETAMINOPHEN                 | OXYCODONE HCL/ACETAMINOPHEN
| OXYCONTIN                               | OXYCODONE HCL
| OXYMORPHONE HCL                         | OXYMORPHONE HCL
| OXYMORPHONE HCL ER                      | OXYMORPHONE HCL
| PENTAZOCINE-NALOXONE HCL                | PENTAZOCINE HCL/NALOXONE HCL
| PERCOCET                                | OXYCODONE HCL/ACETAMINOPHEN
| PRIMLEV                                 | OXYCODONE HCL/ACETAMINOPHEN
| REPREXAIN                               | HYDROCODONE/IBUPROFEN
| ROXICET                                 | OXYCODONE HCL/ACETAMINOPHEN
| ROXICODONE                              | OXYCODONE HCL
|SUBSYS                                   | FENTANYL
| SYNALGOS-DC                             | ASPIRIN/CAFFEIN/DIHYDROCODEINE
| TRAMADOL HCL                            | TRAMADOL HCL
|*TRAMADOL HCL ER                         | TRAMADOL HCL
| TRAMADOL HCL-ACETAMINOPHEN              | TRAMADOL HCL/ACETAMINOPHEN
| TREZIX                                  | ACETAMINOPHEN/CAFF/DIHYDROCOD
| TYLENOL-CODEINE NO.3                    | ACETAMINOPHEN WITH CODEINE
| TYLENOL-CODEINE NO.4                    |ACETAMINOPHEN WITH CODEINE
| ULTRACET                                |TRAMADOL HCL/ACETAMINOPHEN
| ULTRAM                                  | TRAMADOL HCL
| *ULTRAM ER                              | TRAMADOL HCL
|VICODIN                                  | HYDROCODONE/ACETAMINOPHEN
|VICODIN ES                               | HYDROCODONE/ACETAMINOPHEN
|VICODIN HP                               | HYDROCODONE/ACETAMINOPHEN
|VICOPROFEN                               | HYDROCODONE/IBUPROFEN
|*XARTEMIS XR                             | OXYCODONE HCL/ACETAMINOPHEN
|XODOL 10-300                             | HYDROCODONE/ACETAMINOPHEN
|XODOL 7.5-300                            | HYDROCODONE/ACETAMINOPHEN
|*XTAMPZA ER                              | OXYCODONE MYRISTATE
|XYLON 10                                 | HYDROCODONE/IBUPROFEN
|ZAMICET                                  | HYDROCODONE/ACETAMINOPHEN
|*ZOHYDRO ER                              | HYDROCODONE BITARTRATE

---

Note:
*Extended-release opioid.
$Drug name includes NDC identifiers from the Prescriber Drug Category List for opioids as well as NDC identifiers not included in the Prescriber Drug Category List for opioids.$

```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```
