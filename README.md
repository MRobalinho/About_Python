# About_Python
About Python
----
### Help python
>python /?

### Create another conda environement (name_of_my_env)
>conda create -n name_of_my_env python=2.7
<br /> '>activate name_of_my_env 

### Install another version of package
>conda install pandas=0.20.3
<br />or
<br />'>pip install numpy==1.10.4

<br />To install:	Use the command:
<br />The latest version  >	pip install foo --user
<br />A particular version (e.g., foo 1.0.3)>	pip install foo==1.0.3 --user
<br />A minimum version (e.g., foo 2.0)	> pip install 'foo>=2.0' --user

### Verify Python version
run cmd comand as an admnistrator
<br />>python --version
<br />Python 3.4.3

### To Install a package version
python install pandas==version --user commands

------

## Cleaning and Prepping Data with Python for Data Science — Best Practices and Helpful Packages
<br />https://medium.com/@rrfd/cleaning-and-prepping-data-with-python-for-data-science-best-practices-and-helpful-packages-af1edfbe2a3

### Get column names
column_names = df.columns
<br />print(column_names)
### Get column data types
df.dtypes
### Also check if the column is unique
for i in column_names:
<br />  print('{} is unique: {}'.format(i, df[i].is_unique))

### Meanwhile in my old notebooks ...
import os
<br />currDir = os.path.dirname(os.path.realpath("__file__"))
<br />rootDir = os.path.abspath(os.path.join(currDir, '..'))
<br />sys.path.insert(1, rootDir + '/src/funct') # import func package

### Now I can finally import Foo from the funct package
from func import Foo
-----
### Check the index values
df.index.values

### Check if a certain index exists
'foo' in df.index.values

### If index does not exist
df.set_index('column_name_to_use', inplace=True)
