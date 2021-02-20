# Instructions
Low Mass Dijet Scouting with Calo-Scouting Technique
> ps: These instructions have been prepared for the Fermilab LPC infrastructure.

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
cd prod/submitJobsWithCrab3/
```

> ps: `CMSSW_9_4_0` working for all individual three years if it does not work, use `CMSSW_8_0_17` for **2016**, `CMSSW_9_4_0` for **2017** and `CMSSW_10_2_5_patch1` for **2018**.

## Find Proper JSON File

https://twiki.cern.ch/twiki/bin/viewauth/CMS/PdmV2016Analysis
https://twiki.cern.ch/twiki/bin/viewauth/CMS/PdmV2017Analysis
https://twiki.cern.ch/twiki/bin/viewauth/CMS/PdmV2018Analysis
https://twiki.cern.ch/twiki/bin/view/CMS/PdmV


```bash
2016:
wget https://cms-service-dqm.web.cern.ch/cms-service-dqm/CAF/certification/Collisions16/13TeV/Final/Cert_271036-284044_13TeV_PromptReco_Collisions16_JSON.txt .
2017:
wget https://cms-service-dqm.web.cern.ch/cms-service-dqm/CAF/certification/Collisions17/13TeV/Final/Cert_294927-306462_13TeV_PromptReco_Collisions17_JSON.txt .
2018:
wget https://cms-service-dqm.web.cern.ch/cms-service-dqm/CAF/certification/Collisions18/13TeV/PromptReco/Cert_314472-325175_13TeV_PromptReco_Collisions18_JSON.txt .
```

Change the JSON File and other necessary information in the `crab3_template_data.py` file.

## Global Tag

https://twiki.cern.ch/twiki/bin/view/CMSPublic/SWGuideFrontierConditions?redirectedfrom=CMS.SWGuideFrontierConditions#Global_Tags_for_2016_data_taking


```bash
2016:
80X_dataRun2_HLT_v12
2017:
92X_dataRun2_HLT_v7
2018:
101X_dataRun2_HLT_v7
```


```bash
mkdir -p Inputs_ScoutingCaloHT/
cd Inputs_ScoutingCaloHT/
vi InputList_Run2016B-v1_ScoutingCaloHT.txt
```

> Write the following line into the `InputList_Run2016B-v1_ScoutingCaloHT.txt` file and save it.

```bash
/ScoutingCaloHT/Run2017C-v1/RAW -1 80 92X_dataRun2_HLT_v7
```

> Do the same thing for each datasets (2016, 2017 and 2018)
`-1` for analyzing all dataset, `40` is the root size per job, `92X_dataRun2_HLT_v7` is the global tag


## Send the Dataset to the Crab

####2016
```bash
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016B-v2_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016B-v2_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit

python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016C-v2_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016C-v2_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit

python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016D-v2_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016D-v2_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit

python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016E-v2_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016E-v2_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit

python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016F-v1_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016F-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit

python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016G-v1_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016G-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
```

