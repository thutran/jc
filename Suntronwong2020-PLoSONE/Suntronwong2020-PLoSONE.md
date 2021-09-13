# Climate factors influence seasonal influenza activity in Bangkok, Thailand
Suntronwong N, Vichaiwattana P, Klinfueng S, Korkong S, Thongmee T, et al. (2020). PLOS ONE 15(9)

[DOI](https://doi.org/10.1371/journal.pone.0239729) [PDF](https://journals.plos.org/plosone/article/file?id=10.1371/journal.pone.0239729&type=printable)

## Main points:
- Influenza in the tropics does not follow patterns observed in temperate countries.
- Influenza patterns are affected by climate factors: temperature, relative humidity, rainfall.
- Build a model to predict influenza activity:
  - analyzing 2011 - 2017 data (test set) using autoregressive integrated moving average (SARIMA) multivariate analysis
  - predict 2018 (validation)

Strains: 34.2% influenza A(H1N1)pdm09, 46.0% influenza A(H3N2), 19.8% influenza B virus

## Background:
Influenza activity:

Region | Strain  | Preferred temperature | Preferred by rel. humidity | Preferred rainfall 
--- | --- | --- | --- | --- 
Temperate (UK) | A, B | low | low | 
Temperate (CA) | A | low | high |
Tropical (Rep Cote d'Ivoire) | | | | high
Tropical (UG) | H1N1 | | | low
Tropical (Central America) | | (inconsistent) | high | (inconsistent)
Tropical (SEA) | | high (PH, VN) | high (PH, VN) | high (KH, LA, MM, PH, TH)
Bangkok | | yes | yes | no

## Methods
### Data
- ILI samples Jan 2010 - Dec 2018; PCR for influenza A(H1N1)pdm09, A(H3N2) and influenza B
- Monthly average temperature, rainfall, and relative humidity: Jan 2010 - DecS 2018

### Models
- Univariate analysis: influenza month = linear(avg. temperature); influenza month = linear(rel. humudity); influenza month = linear(rainfall)
- Generalized Linear Model (GLM):
  - influenza month = glm(climate, family = Gaussian); link = identity
  - influenza month = glm(confirmed influenza cases, family = Poisson); link = log
- Cross-correlation:
  - corr(incidence, climate)
  - lag_time(subtype_i peak incidence, climate peak)
- Forecast models for 3 separate subtypes and 3 subtypes altogether ~ climate (as independent variables)
- Time series analysis:
  - Univariate: future influenza = linear(past influenza) (???)
  - Multivariate: future influenza = linear(past influenza + climate)
  - Autoregressive Integrated Moving-Average model: predict based on past data, trend = mean + noise

### Results
factor | Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec
--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- 
temperature | lowest | | | highest | highest | | | | | | | | 
rel humidity * | lowest | | | | | | | | highest | highest | | 
rainfall | | | | | | | | | highest |  | | 
influenza | | | | | | | | | H3N2 | H3N2 | | 

- GLM results:
  - First peak: Feb; hot, dry H1N1, B
  - Second peak: Aug-Sep; wet, humid; H1N1, B, H3N2

- ARIMA results:
  - H1N1: no correlation w climate factors; weak neg H3N2 lag 4, strong pos B lag 0-1
  - H3N2: temperature lag 4, r.huminidy lag 1, rainfall lag 1; r.humidity lag 0 shows good correlation in Fig 4 (???)
  - B: temperature lag 4
  - All: temperature lag 4, r.humidity lag 1, rainfall lag 1 --> similar H3N2 ??? is this because H3N2 had the most samples ???