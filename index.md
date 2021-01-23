## Welcome to Dudu's pages

Hi! This is Dudu's website, a personal webpage mained by Kevin, who wants to record some useful notes here. 

## About me
For my publication, please refer to [Google Scholar](https://scholar.google.com/citations?user=dYFXUyoAAAAJ&hl=zh-CN) and [CityU Scholar](https://scholars.cityu.edu.hk/en/persons/wenchong-zhou(e6c7e700-4033-4a0b-8f86-4a07bb91658d).html).
```markdown
Email: zhou.wenchong@yahoo.com
```

## Personal pursue
```markdown
- CFA
- Research
- Industrial
- Photographing
- Education
- Media
- Health
```


## Note list
```markdown
1. Quantum Espresso installation
2. Gromacs installation
3. Other installation
```

## Quantum Espresso installation
Here are the detailed steps for installation of QE 6.0 using gcc complier.
```markdown
Step 1. Download quantum espresso 6.0 and upload to the SEE home directory

Step 2. Enter command to unzip the installation package
tar zxvf q-e-qe-6.0.0.tar.gz

Step 3. Rename the folder to an easy one (optional)

Step 4. Command
cd /home/wczhou3/qe60

Step 5. Load module
module load openmpi/3.1.4_gcc
module list

Step 6. Command for configure
./configure CC=mpicc FC=mpif90 F77=mpif90

Step 7. Install
make all
or
make -j32 pw pp

Around 11 minutes to finish the installation.
Finally, in your scirpt file, include following commands in:
module load openmpi/3.1.4_gcc
setenv LD_LIBRARY_PATH ${LD_LIBRARY_PATH}:/share/apps/intel_xe/mkl/lib/intel64/
```
Note that the pseudo files in the pseudo folder is not complete and you need to add the specific pseudo files in that folder later on.

The example content of the script (name.sh) is shown below:
```markdown
#!/bin/csh
#
#
#PBS -l nodes=1:ppn=16
#PBS -j oe 
#PBS -k oe
#
#******** The lines above must be included in any job script
#******** 'nodes' is number of nodes((max. is 4) and 'ppn' is number of CPU per node(max. is 8).
#Therefore nodes*ppn given the total number of CPU that must specified in 'mpiexec' 
#
#******** (e.g. if nodes=2 and ppn=8, then yield to 'mpiexec -n 16 ./wrf.exe')
#
#******** Max. number of nodes per job is limited to 4 (i.e. 32 CPUs).
#
#This is an example script test.sh
#
#Submit Job: qsub -j oe -k oe ./test.sh
#(Log files could be found at your home directory)
#
#Monitor Job State: qstat
#Where the meaning of 'State' is: 
#	Q -- job is queued   
#	R -- job is running
#  	H -- Job is held
#
#Delete Job: qdel <job number>
#

module load openmpi/3.1.4_gcc
setenv LD_LIBRARY_PATH ${LD_LIBRARY_PATH}:/share/apps/intel_xe/mkl/lib/intel64/

#Must 'cd' to the working directory of the script as shown below to run your job 
#setenv PATH /share/apps/mpich2_ifort-1.3.2/bin/:"$PATH"
#setenv
which mpiexec
module list
cd  /home/wczhou3/LiVO3/Na8

mpiexec  -n  16   /home/wczhou3/qe6/bin/pw.x < Na8V8O24.in > Na8V8O24.out
```
The input file content:
```markdown
&CONTROL
  prefix='Na8',
  outdir='/home/wczhou3/LiVO3/Na8/temp/',
  pseudo_dir='/home/wczhou3/qe6/pseudo/',
  calculation='scf',
  restart_mode='from_scratch',
  nstep=500,
  forc_conv_thr=1.0D-3,
  tprnfor=.true.,
  disk_io='low',
  max_seconds=280.D+3,
  wf_collect=.true.
/
&SYSTEM
  ibrav=0,
  nat=40,
  ntyp=3,
  nspin=2,
  ecutwfc=35.D0,
  ecutrho=350.D0,
  tot_charge=0.0,
  degauss=0.005D0,
  occupations='smearing',
  smearing='mp',
  starting_magnetization(1)=0,
  starting_magnetization(2)=0.1,
  starting_magnetization(3)=0.1,
  lda_plus_u=.true.,
  Hubbard_U(1)=1.e-6,
  Hubbard_U(3)=1.e-6,
/
&ELECTRONS
  startingwfc='atomic+random',
  diago_david_ndim=4,
  conv_thr=1.D-6,
  mixing_beta=0.2D0,
  electron_maxstep=500,
/
&IONS
  ion_dynamics='bfgs',
  upscale=10.0,
/
ATOMIC_SPECIES
V  50.94 V.pbe-spn-rrkjus_psl.0.2.3.UPF
Na 22.99 Na.pbe-spn-rrkjus_psl.0.2.UPF
O  16.00 O.pbe-n-rrkjus_psl.0.1.UPF
ATOMIC_POSITIONS angstrom
V        2.591039845   0.863727017   1.459055326
V        6.098445500   8.604272983   4.117115417
V        7.029705438   0.863728383   1.329030244
V        1.659779908   8.604271617   4.247140500
V        7.867123402   5.597768018   1.459088834
V        0.822361943   3.870231982   4.117081909
V        1.753613801   5.597758803   1.328994951
V        6.935871545   3.870241197   4.247175793
Na       3.879118487   1.985307021   4.182126103
Na       4.810366858   7.482692979   1.394044641
Na      -1.396883610   6.719333882   4.182128132
Na      -0.465631045   2.748666118   1.394042612
Na       4.810367751   3.914045221   1.394052541
Na       3.879117594   5.553954779   4.182118203
Na      -0.465619025   8.647969853   1.394035343
Na      -1.396895630   0.820030147   4.182135401
O        1.020021454   0.973731778   0.918932441
O        7.669463892   8.494268222   4.657238303
O        8.600723758   0.973731513   1.869152848
O        0.088761588   8.494268487   3.707017896
O        6.296071115   5.707712102   0.918963600
O        2.393414231   3.760287898   4.657207144
O        3.324665165   5.707708408   1.869119394
O        5.364820181   3.760291592   3.707051350
O        3.157133113   2.369438843   1.827159789
O        5.532352233   7.098561157   3.749010954
O        6.463610923   2.369436809   0.960926880
O        2.225874423   7.098563191   4.615243864
O        8.433133166   7.103462588   1.827170553
O        0.256352180   2.364537412   3.749000190
O        1.187606165   7.103458239   0.960914817
O        7.501879181   2.364541761   4.615255927
O        3.652127048   0.086417818   0.209085091
O        5.037358297   9.381582182   5.367085653
O        5.968616141   0.086417598   2.579000074
O        2.720869204   9.381582402   2.997170670
O        8.928179817   4.820429217   0.209099888
O       -0.238694472   4.647570783   5.367070856
O        0.692562539   4.820425561   2.578989602
O        7.996922806   4.647574439   2.997181142
K_POINTS automatic
2 2 4 0 0 0
CELL_PARAMETERS angstrom
10.5520000458         0.0000000000         0.0000000000
 0.0000000000         9.4680004120         0.0000000000
-1.8625148323         0.0000000000         5.5761708813
```




## Break Line


## Welcome to Dudu's pages

You can use the [editor on GitHub](https://github.com/KevinChow8/du.github.io/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Hi! This is Dudu's website. I want to record my notes here. 
Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/KevinChow8/du.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
