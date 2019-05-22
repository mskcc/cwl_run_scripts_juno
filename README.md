## Setup to run in JUNO

1. Create a `virtualenv venv` and `source venv/bin/activate`
2. Install toil.
```
git clone https://github.com/mskcc/toil.git
cd toil
git checkout release/3.20.0a1-MSK # mskcc repo has minor change in lsf.py vs. main DataBiosphere toil
make develop extras=[cwl]
```
3. Clone the CWLs repo in some directory
 ```
cd ..
git clone https://github.com/mskcc/cwls
```
4. Export LSF args `export TOIL_LSF_ARGS='-sla CMOPI'`
5. Load Singularity with `module load singularity/3.1.1`

## Running with cwltool

You can locally run the CWLs using `cwltool`.

`cwltool --singularity <cwl file> <input parameters>`

If you have the input parameters in a YAML, you can provide that, as well:

`cwltool --singularity <cwl file> <yaml file>`

## Running with cwltoil

To be added...

## Adding a Singularity Pull directory

To be added...
