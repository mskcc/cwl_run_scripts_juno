## Setup to run in JUNO

Requirements:
- python 2.7.10

1. In some working directory of your choosing, create a `virtualenv venv` and `source venv/bin/activate` 
```
virtualenv venv
source venv/bin/activate
```
2. Install toil.
```
git clone https://github.com/mskcc/toil.git
cd toil
git checkout release/3.20.0a1-MSK # mskcc repo has minor change in lsf.py vs. main DataBiosphere toil'
make develop extras=[cwl]
```
3. Clone which CWLS you want to use into some directory, for example https://github.com/mskcc/cwls
 ```
cd ..
git clone --recursive https://github.com/mskcc/cwls
```

## Running with cwltool

You can locally run the CWLs using `cwltool`.

`cwltool --singularity <cwl file> <input parameters>`

If you have the input parameters in a YAML, you can provide that, as well:

`cwltool --singularity <cwl file> <yaml file>`

## Running with cwltoil

You can have toil submit jobs to the JUNO cluster for you.

Pre-requisites:
1. If you have an SLA, export LSF args to `TOIL_LSF_ARGS`. For SLA Short, for example 
```
export TOIL_LSF_ARGS='-sla Short'
```
You can also add other `bsub` parameters, like walltime `-W`, to `TOIL_LSF_ARGS`.

2. Load Singularity with 
```
module load singularity/3.3.0
```
3. In your working directory, make the `job-stores` and `work` directories:
```
mkdir job-stores work
```

Running:

1. Assuming you have a YAML file ready, you can submit your job to the cluster right away.
```
bash run_script_lsf.sh <path to CWL> <path to YAML> <output directory name>
```

## Adding a Singularity Pull directory

To be added...
