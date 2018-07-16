
===============================================================================



## Predicting Prescriber induced Overdose
--------------------------------------------------------------------------------




**Author : Kiros Gebremariam**
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------
Cohorts of the Data Science Immersive, General Assembly @ Washington DC campus
------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------

=================================================================================

--------------------------------------------------------------------------------------------------------
### DATA SCIENCE IMMERSIVE FINAL CAPSTONE
-------------------------------------------------------------------------------------------------------
=================================================
 

This capestone was initaited with an idea that why are so much more physicians presecribing medications that can lead to overdose. I have worked with patients for more than a year in a clinic as well as a hospital and saw significant amount of patients requesting pain relief medications again and again. I have seen people i know been affected with the chronic and life threatening overdose.

------------------------------------------------------------------------------------------------------------------

The objective of this capestone is to **identify types of prescribers that are a high-risk for opioid related fatalities and predict most influential opioids leading to deaths.**

------------------------------------------------------------------------------------------------------------------

The public health data was extracted from [CDC](https://wonder.cdc.gov/). Downloading data from wonder requires the signing f online conscent and querring the needed information separately and the system will generate the text versions and i have extracting individually for the text versions the deaths associated with opiods. I noticed some anomalies when extracting data from Wonder in large due to the system or functionality of wonder tool they have to group the needed data based on the querry.  The opiods related with Drug enforcement Agency (DEA) licensed specialities connected with the opiods were downloaded from FDA and cross matched with the 2013-2016 Opiods drusglist for the year 2013-2016 can also be accessed [here](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html). The Part D Prescriber PUF file was sas version and in texti downloaded into individual tab separated text files as dowloading the 3.2GB data at once and extracting needs significant processing power besides I noticed some anomalies when extracting data from Wonder in large due to the system or functionality of wonder tool they have to group the needed data. The otherData was extraced from CMS Medicare [Part D Opioid Prescriber Data]( https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/Part-D-Prescriber.html),[cms](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html) and  [NHE](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NationalHealthAccountsStateHealthAccountsProvider.html)

In this notebook, i am going to analyze the datasets i would use for the prediction. In particular, in this note book i will use the Exploratory Data Analysis(eda) in order to understand the statistical structure of the data. Furthermore, in the following notebooks i will build a predictive machine learning model to predict a certain target variable (prescribers) from other attributes that are linked with the features that i will learn from the eda. The datasets are collected from a real world datasets currently available  and they contains a substantial amount of missing values. In this notebook, i will try to set up  my datasets in note book 1.1 and in 1.2 i will cean all the datasets that i will use in the future and try to understand their relationships and in the next notebook. In Notebook 1.3  i will visualize the most important features and associated ones based on the data collected  that will be used for the next work. All the datasets were collected from different sources and validated. Somedatasets are official querried from respective government institutions using private usercode and adjusted to the subject after cleaning.


------------------------------------------------------------------------------------------------------
# Prepare the Data for Modeling and feature importance visual
------------------------------------------------------------------------------------------------------

## Feature Selection
------------------------------------------------------------------------------------------------------

In this section, I will select specific features for model training. The original dataset contains 265 features, most of which are categorical attributes, dominantly the list of drug names that are approved as pain medications that need special AED licensed prescriber.Here,my main target is to predict the overdoses using the  the list of prescriber specialists with NPI information and the FDA approved drug lists. The data set has only total opiod cliams and total claim counts and i took the standard prescription for opiod drugs is 84 days which is 12 weeks. Therefore, an additional feature was created in the data cleaning, pre processing that shows avg_op_supply which i limit to the standard to be 84 and any ones who prescribes the category of medications under the controlled substance act(CSA). The CSA is used for organizing drugs based on the risk of abuse or harm to users in five and my capestone focuses on the approved by [FDA](https://www.fda.gov/drugs/drugsafety/informationbydrugclass/ucm251735.htm) and [DEA](https://www.deadiversion.usdoj.gov/schedules/) to be prescribed by licensed and certified health professional.  These drug lists that are considered controlled substances under the Controlled Substances Act (CSA) are divided into five schedules.  An updated and complete list of the schedules is published annually in [Title 21 Code of Federal Regulations (C.F.R.) §§ 1308.11 through 1308.15](https://www.deadiversion.usdoj.gov/21cfr/cfr/2108cfrt.htm).

Therefore, for analysis and visualization  i only took those physicians who have greater opiod cliams from the center for medical services dataset and created a feature average opiod supply  by dividing the total cliamcount by the total opiod cliam count and reviewed those specialists who prescribe more than the set limit of 12 weeks. The opiod longer feature was created as a new feature that measures the length of opiod prescription supply more than 84 days. As been visualized in notebook 1.3, significant amount of prescribers are family physicians, followed by internal medicine,nurse practitioners, Physicain Assistant and physical medicine and rehabilitation. When i group based on speciality and the vsuals can be accessed   [here top 20](https://plot.ly/~kiros/112),[here state and drug tableau](https://public.tableau.com/profile/kirosdsi.com#!/vizhome/CapstoneUSAOpiodscrisisByStateandSpeciality2018/ByState) and the lists are as follows:-
  > $'Cardiology', 'Nephrology', 'Endocrinology', 'Neurology'  'General Practice', 'Internal Medicine', 'Urology'$,   > $'Pulmonary Disease', 'Gastroenterology', 'Family Practice', 'Infectious Disease','Psychiatry'$ 
  >$'Nurse Practitioner', 'Ophthalmology','Allergy/Immunology', 'Otolaryngology', 'Psychiatry & Neurology'$ , $'Rheumatology', 'Dermatology', 'Obstetrics/Gynecology'$

==========================================================================

**Datasources**
------------------------------------------------------------------------------------

   -  CDC  : 
       -  Current Multiple cause of Death: https://wonder.cdc.gov/mcd-icd10.html
       -  Multiple Cause of Death Data|NCHS: https://wonder.cdc.gov/wonder/help/mcd.html
        -https://www.cdc.gov/nchs/index.htm
        - https://www.kff.org/other/state-indicator/smha-expenditures-per-capita/?currentTimeframe=0&selectedRows=%7B%22wrapups%22:%7B%22united-states%22:%7B%7D%7D%7D&sortModel=%7B%22colId%22:%22Location%22,%22sort%22:%22asc%22%7D
  
   -CMS:  
      - https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NationalHealthAccountsStateHealthAccountsProvider.html
      - https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NationalHealthAccountsStateHealthAccountsProvider.html
      - https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/downloads/dsm-16.pdf
 
   - Medicare Provider Utilization and Payment Data: Part D Prescriber Data CY 2013-2016:
     -  https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/Part-D-Prescriber.html
    - Part D Prescriber Data CY 2016** : https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/PartD2016.html

### Medicare Part D Prescriber Look-up Tool: https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html

### Technical terminologies and definitions can be accessed from the following address:

      - https://www.drugabuse.gov/publications/drugfacts/prescription-opioids
      - https://www.deadiversion.usdoj.gov/21cfr/cfr/2108cfrt.htm

---------------------------------------------------------------------------------------------------------------------------------------
#### Data Dictionary :TBA
=======================================================================================
 |Term                           |  Definition

 |Opioids                       | are a class of drugs naturally found in the opium poppy plan
 
 |common prescription opioids   | hydrocodone (Vicodin®) oxycodone (OxyContin®, Percocet®). oxymorphone (Opana®),morphine (Kadian®,Avinza®)
                                | codeine and fentanyl





### Tableau Visualization 
-----------------------------------------------------------------------------
  - state and speciality based visuals : https://public.tableau.com/profile/kirosdsi.com#!/vizhome/CapstoneUSAOpiodscrisisByStateandSpeciality2018/ByState
  
  
 ### Adverse effects of prescrption Drugs
 ===============================================================================
 
 - https://www.drugfreeworld.org/drugfacts/prescription-drugs.html
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



