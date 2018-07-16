
===============================================================================



## Predicting Prescriber induced Overdose
---------------------------------------------------------------------------------------------------------




**Author : Kiros Gebremariam**
-------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------
Cohorts of the Data Science Immersive, General Assembly @ Washington DC campus
----------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------

=================================================================================

--------------------------------------------------------------------------------------------------------
### DATA SCIENCE IMMERSIVE FINAL CAPSTONE
-------------------------------------------------------------------------------------------------------
=================================================
 
## Introduction: 
------------------------------------------------------------------------------------------------------------
This capestone was initaited with an idea that why are so much more physicians presecribing medications that can lead to overdose. I have worked with patients for more than a year in a clinic as well as a hospital and saw significant amount of patients requesting pain relief medications again and again. I have seen people i know been affected with the chronic and life threatening overdose. This capstone is a supervised training that uses RandomForest Classifier, Logistic Regression, and Neural Networks by using Keras to predict prescriber induced Overdose using datasets from CDC/Winder,CMS and the department of justice. The opiod prescriber is used as a target variable. 

-----------------------------------------------------------------------------------------------------------

The objective of this capestone is to **identify types of prescribers that are a high-risk for opioid related fatalities across the country and predict most influential opioids leading to opiod related deaths.**

-------------------------------------------------------------------------------------------------------------
### Data Cleaning: 

 The dataset for this capstone was collected from CDC,CMS,KAISER FAMILY FOUNDATION. The public health data was extracted from [CDC](https://wonder.cdc.gov/) which is and metadata from 2011 - July 2016. Downloading data from wonder requires the signing f online conscent and querring the needed information separately and the system will generate the text versions and i have extracting individually for the text versions the deaths associated with opiods. I noticed some anomalies when extracting data from Wonder in large due to the system or functionality of wonder tool they have to group the needed data based on the querry.  The opiods related with Drug enforcement Agency (DEA) licensed specialities connected with the opiods were downloaded from FDA and cross matched with the 2013-2016 Opiods drusglist for the year 2013-2016 can also be accessed [here](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html). The Part D Prescriber PUF file was sas version and in texti downloaded into individual tab separated text files as dowloading the 3.2GB data at once and extracting needs significant processing power besides I noticed some anomalies when extracting data from Wonder in large due to the system or functionality of wonder tool they have to group the needed data. The otherData was extraced from CMS Medicare [Part D Opioid Prescriber Data]( https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/Part-D-Prescriber.html),[cms](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html) and  [NHE](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NationalHealthAccountsStateHealthAccountsProvider.html). All the datasets were collected from different sources and validated. Somedatasets are official querried from respective government institutions using private usercode and adjusted to the subject after cleaning. The overall dataset set was cleaned by dropping the unnecessary columns and missing data since the total missing data was very small compared to an overall dataset. In addition, feature engineering was performed by converting the helpful column into a binary classification, opiod prescriber and not opiod prescriber in one column as 1 or 0.
 
### Exploratory Data Analysis

In overll, the opiod prescribing behaviour of health professionals were exponentially increased since opiod epidemic begin in the USA in 1996.The start of the Epidemic according the literatures and the CDC is the FDA approval of the Purdue Pharmaceuticals drugs and OxyContin for non-cancer pain, which caused  the beginning of the epidemics, though purdue pleaded guilty in 2007 and accepted a fine of $635 million fine. Grouping the specialists by the number of prescriptions they give to patients a significant amont of deaths across almost all states were observed. According to the datasets the number of opioid prescriptions dispensed by doctors steadily increased from 112 million prescriptions in 1992 to a peak of 282 million in 2012, since  2012 declined, falling to 236 million in 2016. In 2016, 6.2 billion hydrocodone pills were distributed nationwide. The second most prevalent opioid was oxycodone (Percocet). In 2016, according to the CDC around  5 billion oxycodone tablets were distributed in the United States, which i say it the bells curve,USA is 5% of he worlds population but 80% of the worlds opiods are prescribed here and its easy to see the severity of over prescription of opiates.Based on the dataset the state of california is leading with the highest numebr of deaths due to overdose. Kentucky has been hit particularly hard with 1,419 reported overdose deaths in 2016, which is 33.5 per 100,000 people according to the CDC wonder data and of those deaths 989 which is 23.6 per 100,000 people involved some type of opiods. it was followed by westverginia which is 884 reported  overdose deaths which is 52 per 100,000 people. The full analysis of the data sets and features are presented in notebook 1.3

------------------------------------------------------------------------------------------------------
# Prepare the Data for Modeling and feature importance visual
------------------------------------------------------------------------------------------------------

## Feature Selection
------------------------------------------------------------------------------------------------------

Now we have  more than 265 features but what does they mean or actually how much do we need to know about these features. my Answer to this question would be  not need to know meaning of all the 265 features. What's important is that during the Exploratry data analysis  when we use the `.describe()` for numerical values and the `.describe(include['objects]), which describes all objects' we already have some insights to imagine in our mind we should know something like variance, standart deviation, number of sample (count) or max min values. These type of information helps to understand about what is going on  with the data.  Therfore, standirdization or normalization are important when  before visualization, feature selection, feature extraction or classificaiton. In order to visualizate  the data  in python, its always good to have the jupyter notbook inputs or libraries or packages installed like matplotlib or seaborn or plotly. The plots i used in this capstone are dominantly bar plots, histograms and to some extent maps. The visulization is one of the best methods to understand the data and helps in selecting what features to use for modeling and further extraction or elimination. 

There are mutiple ways that any datascientist would use to select features from the dataset.The methods can range from  feature selection with correlation either using heatmaps or just correlation, univariate feature selection, recursive feature elimination (RFE), recursive feature elimination with cross validation (RFECV) and tree based feature selection. Here i used correlation feature selection. Since my dataset has more than 265 features, most of them drug names. I will select specific features for model training. The original dataset contains 265 features, most of which are categorical attributes, dominantly the list of drug names that are approved as pain medications; that need special AED licensed prescriber.Here,my main target is to predict the overdoses using the  the list of prescriber specialists with NPI information and the FDA approved drug lists. The data set has only total opiod cliams and total claim counts and i took the standard prescription for opiod drugs is 84 days which is 12 weeks. The standards  used to measure the opiod overdose use morphine as gold standard. other drug types of drugs depending on their strength are measured  using morphine milligram equivalents (MME). according to the study by [CDC](https://www.cdc.gov/mmwr/volumes/66/wr/mm6626a4.htm?s_cid=mm6626a4_w) high-dose prescribing rates are classified as prescriptions with daily dosage greater than or equal to 90.  Therefore, based on the evidences i got from CDC and KFF i created an additional feature in the data cleaning, pre processing that shows avg_op_supply which i limit to the standard to be 84 days and any ones who prescribes the category of medications under the controlled substance act(CSA). The CSA is used for organizing drugs based on the risk of abuse or harm to users in five and my capestone focuses on the approved by [FDA](https://www.fda.gov/drugs/drugsafety/informationbydrugclass/ucm251735.htm) and [DEA](https://www.deadiversion.usdoj.gov/schedules/) to be prescribed by licensed and certified health professional.  These drug lists that are considered controlled substances under the Controlled Substances Act (CSA) are divided into five schedules.  An updated and complete list of the schedules is published annually in [Title 21 Code of Federal Regulations (C.F.R.) §§ 1308.11 through 1308.15](https://www.deadiversion.usdoj.gov/21cfr/cfr/2108cfrt.htm).

Therefore, for analysis and visualization  i only took those physicians who have greater opiod cliams from the center for medical services dataset and created a feature average opiod supply  by dividing the total cliamcount by the total opiod cliam count and reviewed those specialists who prescribe more than the set limit of 12 weeks. The opiod longer feature was created as a new feature that measures the length of opiod prescription supply more than 84 days. As been visualized in notebook 1.3, significant amount of prescribers are family physicians, followed by internal medicine,nurse practitioners, Physicain Assistant and physical medicine and rehabilitation. When i group based on speciality and the vsuals can be accessed   [here top 20](https://plot.ly/~kiros/112),[here state and drug tableau](https://public.tableau.com/profile/kirosdsi.com#!/vizhome/CapstoneUSAOpiodscrisisByStateandSpeciality2018/ByState) and the lists are as follows:-
  > $'Cardiology', 'Nephrology', 'Endocrinology', 'Neurology'  'General Practice', 'Internal Medicine', 'Urology'$,  
  > $'Pulmonary Disease', 'Gastroenterology', 'Family Practice', 'Infectious Disease','Psychiatry'$ 
  >$'Nurse Practitioner', 'Ophthalmology','Allergy/Immunology', 'Otolaryngology', 'Psychiatry & Neurology'$ , $'Rheumatology', 'Dermatology', 'Obstetrics/Gynecology'$



---------------------------------------------------------------------------------------------------------------

### Models
---------------------------------------------------------------------------------------------------------------
The baseline  of the data set to overcome is 53.7%. Out of all the models (RandomForest Classification, Logistic Regression,Decision tree,Adaboost classifier, TPOTClassifier  and Neural Network using Keras), the Descision tree,random forest neural network out performed baseline and other models with 81% accuracy score on the test dataset. The neural network uses Gender, speciality  as my target variable was binary classification problem, opiod prescriber or not opiod prescriber (0 to 1). The model trained in on 13,125 samples, validate on 4375 samples. The neural network model has the number of inputs as  hidden layers with relu activation function. The output layer uses sigmoid since it is a classification problem. The model compiler uses binary cross-entropy as a loss function, Adam optimizer, and accuracy metrics with an early stop to avoid exhaustive training. I have also used TPOT to see which model has best features and estimators and does not perform much better. The models i run to predict the opiod prescribers usinig binary method can be accesed in  notebooks 1.4 to 1.6.

------------------------------------------------------------------------------------------------------------------
### Conclusion
------------------------------------------------------------------------------------------------------------------
The opiod epidemic is increasing at alaring rate. Drug overdoses account for a significant portion of accidental deaths in adolescents and young adults in the country, which are tomorrow leaders of the nation. The majority of drug overdoses  according to the dataset cross validated from multple sources indicate they involve opioids, a class of inhibitor molecules that disrupt transmission of pain signals through the nervous system. Medically, they are used as powerful pain relievers; however, they also produce feelings of euphoria, which is temporary happiness.. This temporary happiness and avoidance of pain makes the individual to consume more doses than prescribed at the end its highly addictive and prone to abuse. The use of opiods to mitigate or reduce chronic pain is one of the hot and controversial topics nowadays.There is no good studies show long term improved pain scores with chronic opioids rather than the ultimate death of the productive society and care must be taken. The prescription of opiods for only severe pain that sustain more than three months and no other drug mitigates, trying alternative non addictive medications is important, if there is any one taking medication, stoping would be appropriate. The interesting point from multiple sources and KFF datasets indicate most people who are addicted or overdesed and visited the emergency room got the medication from friends or from strangers , which indicates the prescription drugs quantity prescribed should not be more than the recommended and ther msu also exst a mechanism to remove left over pills like  either returning to the facility so that they will be removed with the hazardous wastes or submitting to the local police.





===================================================================================

### Datasources
-------------------------------------------------------------------------------------------------------

   -  CDC  : 
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

 Medicare Part D [Prescriber Look-up]( https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html)

### Technical terminologies and definitions can be accessed from the following address:

      .[prescription-opioids]( https://www.drugabuse.gov/publications/drugfacts/prescription-opioids)
      .[SCHEDULES OF CONTROLLED SUBSTANCES]( https://www.deadiversion.usdoj.gov/21cfr/cfr/2108cfrt.htm)

---------------------------------------------------------------------------------------------------------------------------------------
#### Data Dictionary :
=======================================================================================
 |Term                           |  Definition

 |Opioids                       | are a class of drugs naturally found in the opium poppy plan
 
 |common prescription opioids   | hydrocodone (Vicodin®) oxycodone (OxyContin®, Percocet®). oxymorphone (Opana®),morphine (Kadian®,Avinza®)
                                | codeine and fentanyl





### Tableau Visualization 
-----------------------------------------------------------------------------
  - [State and speciality based visuals](https://public.tableau.com/profile/kirosdsi.com#!/vizhome/CapstoneUSAOpiodscrisisByStateandSpeciality2018/ByState)
  
  
 ### Adverse effects of prescrption Drugs
 ===============================================================================
 
 
 - [impact of prescription](https://www.drugfreeworld.org/drugfacts/prescription-drugs.html)
  - 

### Part D Prescriber- Opioids List of Drugs



---------------------------------------------------------------------------------------------

|Drug Name                              | Generic Name

-----------------------------------------------------------------------------------------------

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

------------------------------------------------------------------------------------
Note:
*Extended-release opioid.
$Drug name includes NDC identifiers from the Prescriber Drug Category List for opioids as well as NDC identifiers not included in the Prescriber Drug Category List for opioids.$


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
