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
