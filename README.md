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


