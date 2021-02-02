# Python utilities

### Imports
```python
import pandas as pd
import numpy as np
```
### Change display number of rows or columns:
```python
pd.set_option('display.max_rows', 1000)
pd.set_option('display.max_columns', 1000)
```
### to remove SettingWithCopyWarning:
```python
pd.set_option('mode.chained_assignment', None)
```

### To remove possible whitespaces (tabs) on the dataframe:
```python
df = df.apply(lambda x: x.str.strip() if x.dtype == "object" else x)
```
### Print column names:
```python
cols = table_imptt.columns.tolist()
print(cols)
```
```python
cols = list(bbtools.columns)
print('", "'.join(cols))
```
### Statistics
```python
statistics = df.describe().loc[["mean", "std", "min", "25%", "50%", "75%", "max"]].round(2)
```
* * *

* * *
## Scripts
### Script with pass arguments
```python
import argparse
parser = argparse.ArgumentParser(description='Move bins according to taxonomy')
parser.add_argument("taxonomy", help="File with gtdb result")
args = parser.parse_args()
print("\n")
print("Using:")
print("~ Taxonomy: {}".format(args.taxonomy))
```
### get current directory
os.getcwd()
### change directory
os.chdir("/home/gomes/silva/Liu_et.al_2020/bins")

### basic file creation
```python
with open(args.taxonomy, "r+") as f:
    lines = f.readlines()
f.close()
```

### append to dictionary
```python
if x not in d.keys():
    d[x] = y
elif x in d.keys():
    d[x].append(y)
```
