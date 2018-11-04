# About_Python
About Python
----
### Help python
>python /?

### Create another conda environement (name_of_my_env)
>conda create -n name_of_my_env python=2.7
<br /> '>activate name_of_my_env 

### Verify instaled Conda environements
<br />CMD.exe  (as admnistrator )
<br />conda info --envs

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
### Rename  a conda environment
<br />conda create --name new_name --clone old_name
<br />Root environment is named as base, You can use following command:
<br />conda create --name <env_name> --clone base

### List all the packages installed in conda environment and his version
<br />conda list -n <env_name>

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

## np.where(if_this_is_true, do_this, else_do_that)
<br/>Follow this syntax:
<br/>np.where(if_this_condition_is_true, do_this, else_this)
<br/>Example:
<br/>df['new_column'] = np.where(df[i] > 10, 'foo', 'bar) 

## Assert
<br/>Simple dataframe to test:
<br/>df = pd.DataFrame(data={'col1':np.random.randint(0, 10, 10), 'col2':np.random.randint(-10, 10, 10)})
<br/>
<br/> Index   col1  col2
<br/>0     0     6
<br/>1     6    -1
<br/>2     8     4
<br/>3     0     5
<br/>4     3    -7
<br/>5     4    -5
<br/>6     3   -10
<br/>7     9    -8
<br/>8     0     4
<br/>9     7    -4
<br/>
<br/>test if all the values in col1 are >= 0 by using the built in method assert
<br/>assert(df['col1'] >= 0 ).all() # Should return nothing

<br/>Let’s test is any of the values are strings.
<br/>assert(df['col1'] != str).any() # Should return nothing

<br/>Testing the two columns to see if they are equal
<br/>assert(df['col1'] == df['col2']).all()

## Package pandas also includes a testing package
<br/>import pandas.util.testing as tm
<br/>tm.assert_series_equal(df['col1'], df['col2'])
<br/>
<br/>AssertionError: Series are different
<br/>Series values are different (100.0 %)
<br/>[left]:  [0, 6, 8, 0, 3, 4, 3, 9, 0, 7]
<br/>[right]: [6, -1, 4, 5, -7, -5, -10, -8, 4, -4]

## The beautifier package 
Is able to help you clean up some commonly used patterns for emails or URLs. It’s nothing fancy but can quickly help with clean up.
<br/>pip3 install beautifier
<br/>from beautifier import Email, Url
<br/>email_string = 'foo@bar.com'
<br/>email = Email(email_string)
<br/>print(email.domain)
<br/>print(email.username)
<br/>print(email.is_free_email)
<br/>>>
<br/>bar.com
<br/>foo
<br/>False
<br/>url_string = 'https://github.com/labtocat/beautifier/blob/master/beautifier/__init__.py'
<br/>url = Url(url_string)
<br/>print(url.param)
<br/>print(url.username)
<br/>print(url.domain)
<br/>>>
<br/>None
<br/>{'msg': 'feature is currently available only with linkedin urls'}
<br/>github.com

## Dedupe

<br/>This is a library that uses machine learning to perform de-duplication and entity resolution quickly on structured data. 
<br/> More information in https://medium.com/district-data-labs/basics-of-entity-resolution-with-python-and-dedupe-bc87440b64d4

<br/> Set fields 
<br/>fields = [
<br/>       {'field' : 'Source', 'type': 'Set'},
<br/>       {'field' : 'Site name', 'type': 'String'},
<br/>       {'field' : 'Address', 'type': 'String'},
<br/>       {'field' : 'Zip', 'type': 'Exact', 'has missing' : True},
<br/>       {'field' : 'Phone', 'type': 'String', 'has missing' : True},
<br/>       {'field' : 'Email Address', 'type': 'String', 'has missing' : True},
<br/>        ]

<br/>Pass in our model
<br/>deduper = dedupe.Dedupe(fields)
<br/> Check if it is working
<br/>deduper
<br/>>>
<br/><dedupe.api.Dedupe at 0x11535bbe0>
<br/> Feed some sample data in ... 15000 records
<br/>deduper.sample(df, 15000)

<br/>dedupe.consoleLabel(deduper)

