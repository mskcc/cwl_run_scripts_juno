## Setup to run in JUNO

Requirements:
- python 2.7.10
- A way to make a virtualenv

1. In some working directory of your choosing, create a `virtualenv venv` and `source venv/bin/activate` 
```
virtualenv venv
```

If you don't have `virtualenv`, you can install it with the following:

```
curl -O https://files.pythonhosted.org/packages/66/f0/6867af06d2e2f511e4e1d7094ff663acdebc4f15d4a0cb0fed1007395124/virtualenv-16.7.5.tar.gz
tar xvfz virtualenv-16.7.5.tar.gz
cd virtualenv-16.7.5
python virtualenv.py venv
```

Then `source` it:

```
source venv/bin/activate
```

2. Install toil.
```
git clone https://github.com/mskcc/toil.git
cd toil
git checkout 3.19.0 # mskcc repo has minor change in lsf.py vs. main DataBiosphere toil
make develop extras=[cwl]
```

NOTE: `git checkout` version changed to `3.19.0` from `release/3.20.0a1-MSK` for stability and compatibility with ROSLIN; you may still use `git checkout 3.20.0a1-MSK` if you are not using ROSLIN. This should be fixed in future versions of `toil`.

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
## output directory name is relative to current working directory
bash run_script_lsf.sh <path to CWL> <path to YAML> <output directory name> 
```
