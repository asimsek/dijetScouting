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

# Step #1
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


## Send the Dataset to the Crab

#### 2016
```bash
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016B-v2_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016B-v2_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016C-v2_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016C-v2_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016D-v2_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016D-v2_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016E-v2_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016E-v2_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016F-v1_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016F-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2016G-v1_12Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2016G-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
```

#### 2017

```bash
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2017C-v1_Jan-28-2020 -i Inputs_ScoutingCaloHT/InputList_Run2017C-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2017D-v1_Jan-28-2020 -i Inputs_ScoutingCaloHT/InputList_Run2017D-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2017E-v1_Jan-28-2020 -i Inputs_ScoutingCaloHT/InputList_Run2017E-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2017F-v1_Jan-28-2020 -i Inputs_ScoutingCaloHT/InputList_Run2017F-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
```


#### 2018

```bash
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2018A-v1_27Feb2020 -i Inputs_ScoutingCaloHT/InputList_Run2018A-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2018B-v1_04April2020 -i Inputs_ScoutingCaloHT/InputList_Run2018B-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2018C-v1_04April2020 -i Inputs_ScoutingCaloHT/InputList_Run2018C-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
python createAndSubmitCrab.py -d Output_ScoutingCaloHT -v ScoutingCaloHT_Run2018D-v1_04April2020 -i Inputs_ScoutingCaloHT/InputList_Run2018D-v1_ScoutingCaloHT.txt -t crab3_template_data.py -c ../flat-data-calo_cfg.py --submit
```


## Find the Processed Lumi (Only CERN Lxplus - not working on LPC)


#### Create Processed Lumi File from Crab (LPC)

```bash
crab report -d Output_ScoutingCaloHT/ScoutingCaloHT_Run201*_*********_********_****
```
> This will create `processedLumis.json` file under this path: `workdir/crab_ScoutingCaloHT__Run*__RAW/results/`

> You need to copy your processed Lumi json file to your lxplus area


#### Setup BRIL-CALC (lxplus)
```bash
cd
cd .local/bin/
export PATH=$HOME/.local/bin:/afs/cern.ch/cms/lumi/brilconda-1.1.7/bin:$PATH
pip install --install-option="--prefix=$HOME/.local" brilws
```


#### Copy `processedLumis.json` file to your lxplus area (LPC)

```bash
scp -r processedLumis.json <username>@lxplus.cern.ch:.local/bin/201*_processedLumis.json
```

#### Find the Processed Lumi Value (lxplus)

```bash
brilcalc lumi -b "STABLE BEAMS" --byls --normtag /cvmfs/cms-bril.cern.ch/cms-lumi-pog/Normtags/normtag_PHYSICS.json -i 201*_processedLumis.json -u /fb
```

> ps: don't forget to change the name of `processedLumis.json` file in command lines



# Step #2

> We created the root files from the datasets in step #1. 
> In step #2, our goal is to pass these root files through certain selection criteria and apply the necessary JECs.

## Condor Instructions (Reduced NTuple)

```bash
cd CMSSW_9_4_0/src/CMSDIJET/
cp -r /uscms_data/d3/asimsek/DiJet2018/CMSSW_9_4_0/src/CMSDIJET/DijetRootTreeAnalyzer/ .
cd DijetRootTreeAnalyzer/
cmsenv
scram b -j 4
voms-proxy-init --voms cms --valid 300:00
```

## Create List From Big NTuples

> ps: change the path of the big ntuple files and create list of the big ntuple roots

**2016**
```bash
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016B-v2__RAW/200212_185539/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016B-v2.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016C-v2__RAW/200212_205441/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016C-v2.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016D-v2__RAW/200212_210139/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016D-v2.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016E-v2__RAW/200212_213500/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016E-v2.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016F-v1__RAW/200212_214158/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016F-v1.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016G-v1__RAW/200212_214338/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016G-v1.txt
```

**2017**

```bash
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2017/ScoutingCaloHT/crab_ScoutingCaloHT__Run2017C-v1__RAW/200128_222324/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2017C-v1.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2017/ScoutingCaloHT/crab_ScoutingCaloHT__Run2017D-v1__RAW/200129_152702/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2017D-v1.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2017/ScoutingCaloHT/crab_ScoutingCaloHT__Run2017E-v1__RAW/200129_155404/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2017E-v1.txt
ls -v1 /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2017/ScoutingCaloHT/crab_ScoutingCaloHT__Run2017F-v1__RAW/200129_155659/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2017F-v1.txt
```


**2018**

```bash
ls -1 /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2018/ScoutingCaloHT/crab_ScoutingCaloHT__Run2018A-v1__RAW/200227_222554/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2018A-v1.txt
ls -1 /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2018/ScoutingCaloHT/crab_ScoutingCaloHT__Run2018B-v1__RAW/200404_195335/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2018B-v1.txt
ls -1 /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2018/ScoutingCaloHT/crab_ScoutingCaloHT__Run2018C-v1__RAW/200404_081100/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2018C-v1.txt
ls -1 /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2018/ScoutingCaloHT/crab_ScoutingCaloHT__Run2018D-v1__RAW/200405_044054/0000/*.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2018D-v1.txt
```


## Before sending the condor

```bash
cd dijetCondor
rm makeMcJobs
vi makeMcJobs.cc
```
> Change the 3 paths in the `makeMcJobs.cc` file according to your own lpc area. (batchSubmitDir, yPARAM2)


> Change year, dataset type, path for the root files to be created, etc. in the `tmpSH_v01.csh` file


```bash
vi tmpSH_v01.csh
```

**Compile the script:**
```bash
g++ `root-config --cflags` -o makeMcJobs makeMcJobs.cc `root-config --glibs` 
```

> Make necessary changes to the following files if you're using different CMSSW version or JSON file.

```bash
vi prepareCondor.csh -> Change CMSSW version (if necessary!)
vi checkJobdir.csh -> Change CMSSW & Json File.
vi tmpJDL_v01.jdl -> Change CMSSW version and Json File.
```

## Set root paths into the rootNtupleClass.h File

> **Note: You should use the following codes separately according to the dataset you will analyze. ie. only first command line of 2016 commands for 2016B**
> ./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016B-v2__RAW/200212_185539/0000/ScoutingCaloHT__Run2016B-v2__RAW_1.root -t dijetscouting/events

**2016**
```bash
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016B-v2__RAW/200212_185539/0000/ScoutingCaloHT__Run2016B-v2__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016C-v2__RAW/200212_205441/0000/ScoutingCaloHT__Run2016C-v2__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016D-v2__RAW/200212_210139/0000/ScoutingCaloHT__Run2016D-v2__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016E-v2__RAW/200212_213500/0000/ScoutingCaloHT__Run2016E-v2__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016F-v1__RAW/200212_214158/0000/ScoutingCaloHT__Run2016F-v1__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2016/ScoutingCaloHT/crab_ScoutingCaloHT__Run2016G-v1__RAW/200212_214338/0000/ScoutingCaloHT__Run2016G-v1__RAW_1.root -t dijetscouting/events
```

**2017**
```bash
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2017/ScoutingCaloHT/crab_ScoutingCaloHT__Run2017C-v1__RAW/200128_222324/0000/ScoutingCaloHT__Run2017C-v1__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2017/ScoutingCaloHT/crab_ScoutingCaloHT__Run2017D-v1__RAW/200129_152702/0000/ScoutingCaloHT__Run2017D-v1__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2017/ScoutingCaloHT/crab_ScoutingCaloHT__Run2017E-v1__RAW/200129_155404/0000/ScoutingCaloHT__Run2017E-v1__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2017/ScoutingCaloHT/crab_ScoutingCaloHT__Run2017F-v1__RAW/200129_155659/0000/ScoutingCaloHT__Run2017F-v1__RAW_1.root -t dijetscouting/events
```

**2018**
```bash
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2018/ScoutingCaloHT/crab_ScoutingCaloHT__Run2018A-v1__RAW/200227_222554/0000/ScoutingCaloHT__Run2018A-v1__RAW_1.root -t dijetscouting/events
- ./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2018/ScoutingCaloHT/crab_ScoutingCaloHT__Run2018B-v1__RAW/200404_195335/0000/ScoutingCaloHT__Run2018B-v1__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2018/ScoutingCaloHT/crab_ScoutingCaloHT__Run2018C-v1__RAW/200404_081100/0000/ScoutingCaloHT__Run2018C-v1__RAW_1.root -t dijetscouting/events
./scripts/make_rootNtupleClass.sh -f /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_big/2018/ScoutingCaloHT/crab_ScoutingCaloHT__Run2018D-v1__RAW/200405_044054/0000/ScoutingCaloHT__Run2018D-v1__RAW_1.root -t dijetscouting/events
```





