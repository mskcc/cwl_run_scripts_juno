## Setup

1. Create a `virtualenv`
2. Install toil.
```
git clone https://github.com/mskcc/toil.git
cd toil
git checkout release/3.20.0a1-MSK # mskcc repo has minor change in lsf.py vs. main DataBiosphere toil
python setup.py install
```
3. Put the CWLs repo in some directory ```
cd ..
git clone https://github.com/mskcc/cwls```
4. Export LSF args `export TOIL_LSF_ARGS='-sla CMOPI'`
