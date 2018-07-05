
# The Predicting Overdose Epidemics in the US


**Datasources**
   -  CDC  : 
       -  Current Multiple cause of Death: https://wonder.cdc.gov/mcd-icd10.html
       -  Multiple Cause of Death Data|NCHS: https://wonder.cdc.gov/wonder/help/mcd.html
        -https://www.cdc.gov/nchs/index.htm
        - https://www.kff.org/other/state-indicator/smha-expenditures-per-capita/?currentTimeframe=0&selectedRows=%7B%22wrapups%22:%7B%22united-states%22:%7B%7D%7D%7D&sortModel=%7B%22colId%22:%22Location%22,%22sort%22:%22asc%22%7D
  
   -CMS:  
      - https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NationalHealthAccountsStateHealthAccountsProvider.html
      - https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/NationalHealthExpendData/NationalHealthAccountsStateHealthAccountsProvider.html
 
   - Medicare Provider Utilization and Payment Data: Part D Prescriber Data CY 2013-2016:
     -  https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/Part-D-Prescriber.html

      -The Part D Prescriber Public Use File (PUF) provides information on prescription drugs prescribed by individual physicians and other health care providers and paid for under the Medicare Part D Prescription Drug Program. The Part D Prescriber PUF is based on information from CMS’s Chronic Conditions Data Warehouse, which contains Prescription Drug Event records submitted by Medicare Advantage Prescription Drug (MAPD) plans and by stand-alone Prescription Drug Plans (PDP).  The dataset identifies providers by their National Provider Identifier (NPI) and the specific prescriptions that were dispensed at their direction, listed by brand name (if applicable) and generic name.  For each prescriber and drug, the dataset includes the total number of prescriptions that were dispensed, which include original prescriptions and any refills, and the total drug cost.  The total drug cost includes the ingredient cost of the medication, dispensing fees, sales tax, and any applicable administration fees and is based on the amount paid by the Part D plan, Medicare beneficiary, government subsidies, and any other third-party payers. Although the Part D Prescriber PUF has a wealth of information on payment and utilization for Medicare Part D prescriptions, the dataset has a number of limitations.  Of particular importance is the fact that the data may not be representative of a physician’s entire practice or all of Medicare as it only includes information on beneficiaries enrolled in the Medicare Part D prescription drug program (i.e., approximately two-thirds of all Medicare beneficiaries).  In addition, the data are not intended to indicate the quality of care provided.  


**Part D Prescriber Data CY 2016** : https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/PartD2016.html

    The Part D Prescriber Public Use File (PUF) provides information on prescription drugs prescribed by individual physicians and other health care providers and paid for under the Medicare Part D Prescription Drug Program. T

### Medicare Part D Prescriber Look-up Tool: https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/OpioidMap.html

      Medicare Part D Opioid Prescribing Mapping Tool
      The Medicare Part D opioid prescribing mapping tool is an interactive tool that shows geographic comparisons, at the state, county, and ZIP code levels, of de-identified Medicare Part D opioid prescription claims – prescriptions written and then submitted to be filled – within the United States. The mapping tool presents Medicare Part D opioid prescribing rates for 2016 as well as the change in opioid prescribing rates from 2013 to 2016.

      T

## accessing the CMS datasets: 

       The CMS datasets can be done either directly downloading the Xlsx spreadshits, or going to the API and requesting the API to give you in what ever format of your interest.  The API format can be accesssed via the following address:
       https://dev.socrata.com/foundry/data.cms.gov/mm6p-bnrx
       
       The Multiple Cause of Death data available on WONDER are county-level national mortality and population data spanning the years 1999-2016. Data are based on death certificates for U.S. residents. Each death certificate contains a single underlying cause of death, up to twenty additional multiple causes, and demographic data. The number of deaths, crude death rates, age-adjusted death rates and 95% confidence intervals for death rates can be obtained by cause of death (4 digit ICD-10 codes, 113 selected causes of death, 130 selected causes of infant death, drug and alcohol related causes of death, injury intent and injury mechanism categories), place of residence (national, region, division, state, and county), age (single-year-of age, 5-year age groups, 10-year age groups and infant age groups), race (American Indian or Alaskan Native, Asian/Pacific Islander, Black or African American, White), Hispanic ethnicity, gender and year. Data are also available by place of death, month and week day of death, and whether an autopsy was performed. Effective April 7, 2011 for Multiple Cause of Death mortality data on CDC WONDER:  data for the "Not Stated" age category or the "Not Stated" Hispanic Origin category cannot be combined with any other specified age group or Hispanic Origin categories.

**Population data**
    The population estimates are U.S. Census Bureau estimates of U.S. national, state, and county resident populations. The year 1999 population estimates are bridged-race intercensal estimates of the July 1 resident population, based on the 1990 and the year 2000 census counts. The year 2000 and year 2010 population estimates are April 1 modified census counts, with bridged-race categories. The year 2011-2016 population estimates are bridged-race postcensal estimates of the July 1 resident population. The 2001 - 2009 population estimates are bridged-race revised intercensal estimates of the July 1 resident population, based on the year 2000 and the year 2010 census counts (released by NCHS on 10/26/2012). The 2001 - 2009 archive population estimates are bridged-race postcensal estimates of the July 1 resident population. For more information, see Population Data Sources. NCHS live-birth data are included for "Infant Age Groups" so that infant mortality rates can be calculated. The number of live births and the population estimate for the "under one year of age" group differ slightly, thus death rates may differ slightly when compared. For more information, see Mortality for Infants. Crude Rates are expressed as the number of deaths reported each calendar year per the factor you select. The default factor is per 100,000 population, reporting the death rate per 100,000 persons.

                    Crude Rate = Count / Population * 100,000





2010 Population Estimates
National, state, and county population estimates are from the U.S. Census Bureau April 1, bridged modified race 2010 Census counts. The original census counts were modified by the U.S. Census Bureau to assign persons who reported their race as "other " to one of the 31 single or multiple-race groups specified in the Office of Management and Budget (OMB) 1997 Standards on Race and Ethnicity. The resulting counts were then bridged to (made consistent with) the four single-race categories on the 1990 Census (White, Black, American Indian or Alaska Native, and Asian or Pacific Islander).

2011 Population Estimates
National, state, and county population estimates are July 1 resident population estimates from the Vintage 2011 bridged-race postcensal series (released by NCHS on 7/18/2012). The bridged-race population files have estimates for the four single-race categories (White, Black, American Indian or Alaska Native, and Asian or Pacific Islander). The postcensal July 1st population estimates are based on the year 2010 April 1st Census counts.

The national, region, division, and state estimates were obtained by summing the county estimates, so the region, division, state and county estimates are consistent with each other within a given year.

2012 Population Estimates
National, state, and county population estimates are July 1 resident population estimates from the Vintage 2012 bridged-race postcensal series (released by NCHS on 6/13/2013). The bridged-race population files have estimates for the four single-race categories (White, Black, American Indian or Alaska Native, and Asian or Pacific Islander). The postcensal July 1st population estimates are based on the year 2010 April 1st Census counts.

The national, region, division, and state estimates were obtained by summing the county estimates, so the region, division, state and county estimates are consistent with each other within a given year.

2013 Population Estimates
National, state, and county population estimates are July 1 resident population estimates from the Vintage 2013 bridged-race postcensal series (released by NCHS on 6/26/2014). The bridged-race population files have estimates for the four single-race categories (White, Black, American Indian or Alaska Native, and Asian or Pacific Islander). The postcensal July 1st population estimates are based on the year 2010 April 1st Census counts.

The national, region, division, and state estimates were obtained by summing the county estimates, so the region, division, state and county estimates are consistent with each other within a given year.

2014 Population Estimates
National, state, and county population estimates are July 1 resident population estimates from the Vintage 2014 bridged-race postcensal series (released by NCHS on 6/30/2015). The bridged-race population files have estimates for the four single-race categories (White, Black, American Indian or Alaska Native, and Asian or Pacific Islander). The postcensal July 1st population estimates are based on the year 2010 April 1st Census counts.

The national, region, division, and state estimates were obtained by summing the county estimates, so the region, division, state and county estimates are consistent with each other within a given year.

2015 Population Estimates
National, state, and county population estimates are July 1 resident population estimates from the Vintage 2015 bridged-race postcensal series (released by NCHS on 6/28/2016). The bridged-race population files have estimates for the four single-race categories (White, Black, American Indian or Alaska Native, and Asian or Pacific Islander). The postcensal July 1st population estimates are based on the year 2010 April 1st Census counts.

The national, region, division, and state estimates were obtained by summing the county estimates, so the region, division, state and county estimates are consistent with each other within a given year.

**2016 Population Estimates**
National, state, and county population estimates are July 1 resident population estimates from the Vintage 2016 bridged-race postcensal series (released by NCHS on 6/26/2017). The bridged-race population files have estimates for the four single-race categories (White, Black, American Indian or Alaska Native, and Asian or Pacific Islander). The postcensal July 1st population estimates are based on the year 2010 April 1st Census counts. The national, region, division, and state estimates were obtained by summing the county estimates, so the region, division, state and county estimates are consistent with each other within a given year.

Comparison with other releases: The current rates and population figures for years 2001-2009 are different from the previous release of these data on CDC WONDER. A different series of population estimates is currently used to calculate rates for 2001-2009. Current population figures for years 2001-2009, other than the infant age groups, are bridged-race estimates of the July 1 resident population, from the revised intercensal county-level 2000-2009 series, released by NCHS on October 26, 2012.

Archive population figures for 2001-2009, other than the infant age groups, are postcensal bridged-race estimates of the July 1 resident population. Archive rates and population figures for years 2001-2009 match NCHS mortality reports published in that time period, but differ slightly from reports published after 2009, because later reports are calculated with more recently produced population estimates for those years. Archive 2001-2004 Population Estimates in the Archive 1999-2004 Data
The archive population estimates for 2001 - 2004 are July 1 resident population estimates from the U.S. Census Bureau's bridged-race postcensal series.

## Archive 2001-2009 Population Estimates:
The archive population estimates for 2001 - 2009 are July 1 resident population estimates from the U.S. Census Bureau's bridged-race postcensal series. The bridged-race population files have estimates for the four single-race categories (White, Black, American Indian or Alaska Native, and Asian or Pacific Islander). The national, region, division, state and county population figures for 2001 - 2009 are county-level bridged-race postcensal estimates of the July 1 resident population from the corresponding postcensal series: 2001 and 2002 from the Vintage 2002 series, 2003 from the Vintage 2003 series, 2004 from the Vintage 2004 series, 2005 from the Vintage 2005 series, 2006 from the Vintage 2006 series, 2007 from the Vintage 2007 series, 2008 from the Vintage 2008 series, and 2009 from the Vintage 2009 series.

The national, region, division, and state estimates were obtained by summing the county estimates, so the region, division, state and county estimates are consistent with each other within a given year. The population estimates correspond to the series that was used when NCHS published the "Final Report" for deaths in the given year, except for year 2001, because detailed population estimates are not available until the 2002 series.

See Comparison with Other Releases for more information, and instruction on how to reproduce archive rates and populations.

## About population migration due to hurricanes in 2005: 
The state and county population estimates for Alabama, Louisiana, Mississippi and Texas reflect population changes that occurred after Hurricane Katrina and Rita in 2005. To accommodate geographic shifts of the Alabama, Louisiana, Mississippi, and Texas populations resulting from Hurricanes Katrina and Rita in 2005, the U.S. Census Bureau developed adjustments in the methodology for state and county population estimates. See methodology for more information.

Note: this concern refers to the archive postcensal population estimates for the years 2005-2009.

If you have additional questions about the population estimates, please see U.S. Census Populations With Bridged Race Categories (http://www.cdc.gov/nchs/about/major/dvs/popbridge/popbridge.htm) or contact PopEst@cdc.gov.



How do I get the top 15 leading causes of death in WONDER?
Group results by "15 Leading Causes" to get death counts and rates for the top 15 rankable causes of death, for your selected query criteria. Note that cross-tabulations, zero value death counts, and suppressed values are not permitted when you group results by "15 Leading Causes." When more than one rankable cause of death occurs in the last position, all these causes are shown.

The "leading causes of death" published by the National Center for Health Statistics (NCHS) are also called "rankable causes of death." The rankable causes are a subset of the 113 selected causes of death, and the 130 selected causes of death for infants. A "#" symbol preceding the label indicates a "rankable" cause of death, from the National Center for Health Statistics (NCHS) list of rankable causes of death.

The "15 leading causes of death" and the "rankable causes of death" apply only to the underlying causes of death. These concepts are not used for analysis of the contributing or multiple causes of death.

How are crude death rates calculated in WONDER?
The "crude death rate" is the number of deaths divided by the population, multiplied by 100,000.

**Crude Death Rate = (number of deaths / population) * 100,000**

Note: 100,000 is the default multiplier, other multipliers can be specified in the query.

How are age-adjusted death rates calculated in WONDER?
The age-adjusted rate is calculated by multiplying the age-specific death rate for each age group by the corresponding weight from the specified standard population, summing across all age groups, and then multiplying this result by 100,000 (or whatever multiplier is specified in the query).

**Age-Adjusted Death Rate = Sum of (Age Specific Death Rate * Standard Population weight) * 100,000**

The age-specific death rate is the number of deaths for a given age group divided by the population of that age group.

**Age Specific Death Rate = (number of deaths in age group / population of age group)**

The "standard population weight " for an age group is calculated by dividing the population for the age group by the sum of the populations for all of the age groups in the query. Please see the question below on "children under 1 year" age categories.

**Standard Population Weight = population for age group / sum of age group populations for all age groups in query**

See http://seer.cancer.gov/seerstat/tutorials/aarates/definition.html for a step-by-step tutorial with an example of the calculations.
