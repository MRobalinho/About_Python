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

### Create list comprehension of the columns you want to lose
columns_to_drop = [column_names[i] for i in [1, 3, 5]]

### Drop unwanted columns
df.drop(columns_to_drop, inplace=True, axis=1)

## What To Do With NaN
#### Fill NaN with ' '
df['col'] = df['col'].fillna(' ')
#### Fill NaN with 99
df['col'] = df['col'].fillna(99)
#### Fill NaN with the mean of the column
df['col'] = df['col'].fillna(df['col'].mean())

## Propagate 
<br /> Propagate non-null values forward or backwards by putting method=’pad’ as the method argument. It will fill the next value in the dataframe with the previous non-NaN value. Maybe you just want to fill one value (limit=1)or you want to fill all the values. Whatever it is make sure it is consistent with the rest of your data cleaning.
<br /><b>df = pd.DataFrame(data={'col1':[np.nan, np.nan, 2,3,4, np.nan, np.nan]})</b>
<br />    col1
<br />0   NaN
<br />1   NaN
<br />2   2.0
<br />3   3.0
<br />4   4.0 # This is the value to fill forward
<br />5   NaN
<br />6   NaN
<br /><b>df.fillna(method='pad', limit=1)</b>
<br />    col1
<br />0   NaN
<br />1   NaN
<br />2   2.0
<br />3   3.0
<br />4   4.0
<br />5   4.0 # Filled forward
<br />6   NaN

### Limited to forward filling, but also backfilling with bfill.

<br />Fill the first two NaN values with the first available value
<br /><b>df.fillna(method='bfill')</b>
<br />    col1
<br />0   2.0 # Filled
<br />1   2.0 # Filled
<br />2   2.0 
<br />3   3.0
<br />4   4.0
<br />5   NaN
<br />6   NaN
  
### Drop any rows which have any nans
df.dropna()
### Drop columns that have any nans
df.dropna(axis=1)
### Only drop columns which have at least 90% non-NaNs
df.dropna(thresh=int(df.shape[0] * .9), axis=1)
<br/>The parameter thresh=N requires that a column has at least N non-NaNs to survive. 
