# Instructions
Low Mass Dijet Scouting with Calo-Scouting Technique
###### ps: These instructions have been prepared for the Fermilab LPC infrastructure.

## Find Datasets for Run-II

https://cmsweb.cern.ch/das/

`dataset status=* dataset=/ScoutingCaloHT/Run201*/RAW`

| 2016 Datasets  | 2017 Datasets | 2018 Datasets |
| ------------ | ------------ | ------------ |
| /ScoutingCaloHT/Run2016B-v2/RAW | /ScoutingCaloHT/Run2017C-v1/RAW | /ScoutingCaloHT/Run2018A-v1/RAW |
| /ScoutingCaloHT/Run2016C-v2/RAW | /ScoutingCaloHT/Run2017D-v1/RAW | /ScoutingCaloHT/Run2018B-v1/RAW |
| /ScoutingCaloHT/Run2016D-v2/RAW | /ScoutingCaloHT/Run2017E-v1/RAW | /ScoutingCaloHT/Run2018C-v1/RAW |
| /ScoutingCaloHT/Run2016E-v2/RAW | /ScoutingCaloHT/Run2017F-v1/RAW | /ScoutingCaloHT/Run2018D-v1/RAW |
| /ScoutingCaloHT/Run2016F-v1/RAW |
| /ScoutingCaloHT/Run2016G-v1/RAW |



## CRAB Instructions (Big NTuple)

```bash
mkdir -p DijetScouting
cd DijetScouting/
cmsrel CMSSW_9_4_0
cd CMSSW_9_4_0/src
cp -r /uscms_data/d3/asimsek/DiJet2018/CMSSW_9_4_0/src/CMSDIJET .
cd CMSDIJET/DijetScoutingRootTreeMaker/
scram b -j 4
cd prod/
```











