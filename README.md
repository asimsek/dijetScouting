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


## Usefull Crab Commands

```bash
crab remake --task <task_id>
crab remake --task 200212_185539:asimsek_crab_ScoutingCaloHT__Run2016B-v2__RAW
```


------------

------------

------------



# Step #2

> There is 1-2% difference between all years in terms of QCD MC samples. Therefore, we used the 2017 QCD MC samples for all years.

## Find MC Datasets for Run-II

https://cmsweb.cern.ch/das/

```
dataset status=* dataset=/QCD_Pt_*to*_TuneCP5_13TeV_pythia8/RunIIFall17DRPremix-PU2017_94X_mc2017_realistic_v11*/AODSIM
```

## MC CRAB Instructions (MC Big NTuple)

```bash
cd CMSSW_9_4_0/src/CMSDIJET/DijetScoutingRootTreeMaker/prod/submitJobsWithCrab3
cmsenv
mkdir -p Inputs_QCD_MC_2017/
vi Inputs_QCD_MC_2017/InputList_QCD_Pt_*to*.txt
```

> Write the following line into the `InputList_QCD_Pt_*to*.txt` file and save it.

```bash
/QCD_Pt_*to*_TuneCP5_13TeV_pythia8/RunIIFall17DRPremix-PU2017_94X_mc2017_realistic_v11_*/AODSIM -1 1 94X_mc2017_realistic_v11
```

> Do the same thing for each mass range (50to80, 80to120, 120to170, 170to300, 300to470, 470to600, 600to800, 800to1000, 1000to1400, 1400to1800, 1800to2400, 2400to3200, 3200toInf)

`-1` for analyzing all dataset, `1` is the root size per job, `94X_mc2017_realistic_v11` is the global tag


## Send MC Datasets to Crab
```bash
python createAndSubmitMC.py -d Output_QCD_MC_2017/ -v QCD_Pt_*to*_02Feb2020 -i Inputs_QCD_MC_2017/InputList_QCD_Pt_*to*.txt -t crab3_template_MC.py -c ../flat-MC-calo_cfg.py --submit
```


------------

------------

------------


# Step #3

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

> ps: Don't forget to change the path of the big ntuple files and create the list of big ntuple roots with following command lines

```bash
cd dijetCondor
```


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
vi prepareCondor.csh -> Change CMSSW version. (if necessary!)
vi checkJobdir.csh -> Change CMSSW & Json File. (if necessary!)
vi tmpJDL_v01.jdl -> Change CMSSW version and Json File. (if necessary!)
```

## Set Root Paths into the rootNtupleClass.h File

> **Note: You should use the following codes separately according to the dataset you will analyze. ie. only first command line of 2016 commands for 2016B**


```bash
cd $CMSSW_BASE/src/CMSDIJET/DijetRootTreeAnalyzer
```

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


## Compile

> You should change the L1,L2,L3 and L2L3Residual JEC file names in `analysisClass_mainDijetCaloScoutingSelection_201*.C` file under `src` folder
> ie. src/analysisClass_mainDijetCaloScoutingSelection_2016.C for 2016B/C/D/E/F/G datasets

> You need to use these command lines for each dataset (2016B, 2016C, 2017D, 2018A,... etc.), each times.

```bash
vi src/analysisClass_mainDijetCaloScoutingSelection_201*.C
```


```bash
ln -sf analysisClass_mainDijetCaloScoutingSelection_201*.C src/analysisClass.C
make clean
make
```

## Create Necessary Files for Condor

```bash
cd dijetCondor
```


```bash
./makeMcJobs <JobName> <bigNtupleRootList.txt>
./makeMcJobs ScoutingCaloHT201*_JEC_AK4CaloHLTL1L2L3_L2L3Residual CaloScoutingHT201*.txt
```


## Send to Condor

```bash
cd bjobsScoutingCaloHT201*_JEC_CaloL1L2L3_PFL2L3Residual_********/
source zz_submitAllScoutingCaloHT201*_JEC_CaloL1L2L3_PFL2L3Residual.csh
```

## Usefull Condor Commands

> Currently there are 3 LPC condors (`lpcschedd1`, `lpcschedd2` and `lpcschedd3`) 
> It is necessary to remove or release them separately.

**Remove All Held Jobs:**
```bash
condor_rm -const 'jobstatus==5' -name lpcschedd1
```

**Hold Reason:**
```bash
condor_q -hold -af HoldReason
```

**Release All Held Jobs (condor will try to execute them, again):**
```bash
condor_release -const 'jobstatus==5' -name lpcschedd1
```

**For more:**
https://uscms.org/uscms_at_work/computing/setup/condor_refactor.shtml#name

**Get rid of the ^M Problem:**
```bash
sed -i -e 's/\r//g' <fileName>
```



# Step #4

> We have produced all the necessary root files so far. Now we can start analyzing.

## Analysis Instruction

```bash
cd DijetScouting/
cmsrel CMSSW_7_4_14
cd CMSSW_7_4_14/src/
cp -r /uscms_data/d3/asimsek/DiJet2018/CMSSW_7_4_14/src/CMSDIJET .
scram b -j 4
cd CMSDIJET/DijetRootTreeAnalyzer
```



## Create List From Reduced Ntuples

```bash
cd scripts/
```

> Don't forget to change the path of the reduced ntuple root files.

**2016**
```bash
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2016/ScoutingCaloHT/ScoutingCaloHT_Run2016B-v2/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016B-v2_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2016/ScoutingCaloHT/ScoutingCaloHT_Run2016C-v2/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016C-v2_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2016/ScoutingCaloHT/ScoutingCaloHT_Run2016D-v2/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016D-v2_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2016/ScoutingCaloHT/ScoutingCaloHT_Run2016E-v2/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016E-v2_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2016/ScoutingCaloHT/ScoutingCaloHT_Run2016F-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016F-v1_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2016/ScoutingCaloHT/ScoutingCaloHT_Run2016G-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2016G-v1_reduced.txt
```

**2017**
```bash
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2017/ScoutingCaloHT/ScoutingCaloHT_Run2017C-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2017C-v1_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2017/ScoutingCaloHT/ScoutingCaloHT_Run2017D-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2017D-v1_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2017/ScoutingCaloHT/ScoutingCaloHT_Run2017E-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2017E-v1_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2017/ScoutingCaloHT/ScoutingCaloHT_Run2017F-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2017F-v1_reduced.txt
```

**2018**
```bash
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2018/ScoutingCaloHT/ScoutingCaloHT_Run2018A-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2018A-v1_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2018/ScoutingCaloHT/ScoutingCaloHT_Run2018B-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2018B-v1_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2018/ScoutingCaloHT/ScoutingCaloHT_Run2018C-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2018C-v1_reduced.txt
ls -1v /eos/uscms/store/group/lpcjj/CaloScouting/rootTrees_reduced/2018/ScoutingCaloHT/ScoutingCaloHT_Run2018D-v1/*_reduced_skim.root | sed -e 's\/eos/uscms\root://cmseos.fnal.gov/\g' > CaloScoutingHT2018D-v1_reduced.txt
```

> Please create all necessary lists. You **don't** need to wait their turn as before.


## Merge the list files

> Please don't forget to check the names of the seperate list files before merging them.

```bash
cat CaloScoutingHT2016*-v*_reduced.txt > CaloScoutingHT2016ALL_reduced.txt
cat CaloScoutingHT2017*-v1_reduced.txt > CaloScoutingHT2017ALL_reduced.txt
cat CaloScoutingHT2018*-v1_reduced.txt > CaloScoutingHT2018ALL_reduced.txt
```


## Kinematic Plots (mjj, eta, phi, DeltaEta, DeltaPhi)

> The following script is creating condor jobs to prepare kinematic plots. 
> You need to change my eos paths with yours.

```bash
source plotterCondor_DatavsMC4.sh <JobName> <DataRootList> <MCRootList> <lumi>

source plotterCondor_DatavsMC4.sh CaloScoutingHT2016ALL_DatavsQDCMC_DE13_M489_wL2L3Residual_26May2020_0009 CaloScoutingHT2016ALL_reduced.txt QCD2017-v1_reduced_new.txt 27225
```



> If you need to produce locally and seperately please use the following command lines. Don't forget to give proper data list, MC list, lumi value etc.

```bash
python DrawFromTree_data4.py --var mjj --xmin 1 --xmax 14000 --xtitle 'Dijet mass [MeV]' --bins 13999 --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --logy --rebin -1 --units GeV
python DrawFromTree_data4.py --var pTWJ_j1 --xmin 30 --xmax 5000 --xtitle 'pT(j1) [GeV]' --bins 200 --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --rebin 5 --units GeV
python DrawFromTree_data4.py --var pTWJ_j2 --xmin 30 --xmax 5000 --xtitle 'pT(j2) [GeV]' --bins 200 --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --rebin 5 --units GeV
python DrawFromTree_data4.py --var etaWJ_j1 --xmin -3 --xmax 3 --xtitle '#eta(j1)' --bins 200 --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --rebin 5
python DrawFromTree_data4.py --var etaWJ_j2 --xmin -3 --xmax 3 --xtitle '#eta(j2)' --bins 200 --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --rebin 5
python DrawFromTree_data4.py --var deltaETAjj --xmin 0 --xmax 1.3 --xtitle '#Delta#eta(jj)' --bins 200 --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --logy --rebin 5
python DrawFromTree_data4.py --var deltaPHIjj --xmin 0 --xmax 3.14 --xtitle '|#Delta#phi(jj)|' --bins 200 --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --logy --rebin 5
python DrawFromTree_data4.py --var phiWJ_j1  --xmin -3.1415 --xmax 3.1415  --xtitle '#phi (j1)' --bins 200  --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --rebin 5
python DrawFromTree_data4.py --var phiWJ_j2  --xmin -3.1415 --xmax 3.1415  --xtitle '#phi (j2)' --bins 200  --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --rebin 5
python DrawFromTree_data4.py --var Dijet_MassAK4 --xmin 1 --xmax 14000 --xtitle 'Dijet Mass AK4 [GeV]' --bins 13999 --rebin -1 --outputDir ${outputFile}/ --inputList_1 ${inputDataList} --inputMC ${inputMC} --lumi ${lumi} --logy --units GeV
```


## Fit

> After having a proper mjj results, you can fit the data with standard dijet fit functions.


```bash
python python/BinnedFit.py -c config/dijet_5param.config -l <lumi> --mass 750_1200_1600 -m gg_qg_qq --xsec 9.5_8.2e-1_2.2e-1 -s <ggResonanceRootFile>,<qgResonanceRootFile>,<qqResonanceRootFile> <eosPathContainingMjjRootFile>/histo_data_mjj_fromTree.root -b <boxName> -d <outputFolder>/<boxName>_dijet_5Param/ --fit-spectrum
```


> Example command lines for all individual years can be found below.

**2016**
```bash
python python/BinnedFit.py -c config/dijet_5param.config -l 27225 --mass 750_1200_1600 -m gg_qg_qq --xsec 9.5_8.2e-1_2.2e-1 -s inputs/ResonanceShapes_gg_13TeV_CaloScouting_Spring16.root,inputs/ResonanceShapes_qg_13TeV_CaloScouting_Spring16.root,inputs/ResonanceShapes_qq_13TeV_CaloScouting_Spring16.root /eos/uscms/store/group/lpcjj/CaloScouting/Plots/CaloScoutingHT2016ALL_DatavsQDCMC_DE13_M489_wL2L3Residual_26May2020_0009/histo_data_mjj_fromTree.root -b CaloDijet2016 -d fits_DE13_wL2L3Residual_27May2020/CaloDijet2016_dijet_5Param/ --fit-spectrum
```

**2017**
```bash
python python/BinnedFit.py -c config/dijet_5param.config -l 35449 --mass 750_1200_1600 -m gg_qg_qq --xsec 9.5_8.2e-1_2.2e-1 -s inputs/ResonanceShapes_gg_13TeV_CaloScouting_Spring16.root,inputs/ResonanceShapes_qg_13TeV_CaloScouting_Spring16.root,inputs/ResonanceShapes_qq_13TeV_CaloScouting_Spring16.root /eos/uscms/store/group/lpcjj/CaloScouting/Plots/CaloScoutingHT2017ALL_DatavsQDCMC_DE13_M489_wL2L3Residual_26May2020_0020/histo_data_mjj_fromTree.root -b CaloDijet2017 -d fits_DE13_wL2L3Residual_27May2020/CaloDijet2017_dijet_5Param/ --fit-spectrum
```

**2018**
```bash
python python/BinnedFit.py -c config/dijet_5param.config -l 59533 --mass 750_1200_1600 -m gg_qg_qq --xsec 9.5_8.2e-1_2.2e-1 -s inputs/ResonanceShapes_gg_13TeV_CaloScouting_Spring16.root,inputs/ResonanceShapes_qg_13TeV_CaloScouting_Spring16.root,inputs/ResonanceShapes_qq_13TeV_CaloScouting_Spring16.root /eos/uscms/store/group/lpcjj/CaloScouting/Plots/CaloScoutingHT2018ALL_DatavsQDCMC_DE13_M489_wL2L3Residual_26May2020_0036/histo_data_mjj_fromTree.root -b CaloDijet2018 -d fits_DE13_wL2L3Residual_27May2020/CaloDijet2018_dijet_5Param/ --fit-spectrum
```



## Scale and Calibrate 2017 and 2018 datasets

> The 2017 and 2018 had different structure. So, we calibrated the 2017 and 2018 datasets with 2016 dataset leaving any systematic fluctuations.


> Don't forget to change eos path of the mjj root file in `CalibrateDataset.py` script.

```bash
python CalibrateDataset.py --year 2017 --lumi 35.449 --root CaloScoutingHT2017ALL_DatavsQDCMC_DE13_M489_wL2L3Residual_26May2020_0020
python CalibrateDataset.py --year 2018 --lumi 59.533 --root CaloScoutingHT2018ALL_DatavsQDCMC_DE13_M489_wL2L3Residual_26May2020_0036
```

## Setting Limits

> Don't forget to make the changes in `findLimitRMax.sh` script (if necessary!).

```bash
source findLimitRMax.sh <configFileName> <year> <Lumi> <rMax> <signalType>
```

**2016**
```bash
source findLimitRMax.sh dijet_5Param 2016 27224 15.4 gg
source findLimitRMax.sh dijet_5Param 2016 27224 15.9 qg
source findLimitRMax.sh dijet_5Param 2016 27224 16.6 qq
```

**2017**

```bash
source findLimitRMax.sh dijet_5Param 2017 35449 2.6 gg
source findLimitRMax.sh dijet_5Param 2017 35449 16.8 qg
source findLimitRMax.sh dijet_5Param 2017 35449 11.4 qq
```

**2018**

```bash
source findLimitRMax.sh dijet_5Param 2018 59533 18.34 gg
source findLimitRMax.sh dijet_5Param 2018 59533 16.5 qg
source findLimitRMax.sh dijet_5Param 2018 59533 19.8 qq
```



## Significance

```bash
source significancePlots.sh gg 2016 27.224 15.4 CaloDijet2016
source significancePlots.sh qg 2016 27.224 15.9 CaloDijet2016
source significancePlots.sh qq 2016 27.224 16.6 CaloDijet2016
```













