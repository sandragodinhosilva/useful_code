# Python utilities

### Remove index name
```python
df = df.rename_axis(None, axis = 1)
```

### Remove percentage
```python
df[col] = df[col].str.rstrip('%').astype('float') / 100.0
```
### Sum per row
```python
df.loc[:,'Total'] = df.sum(numeric_only=True, axis=1)
```
### Count positive values per:
```python
# row
df["Counts"] = len(df.columns) - df.apply(lambda row: sum(row[0:]==0) ,axis=1)
# column
df.loc["Counts",:] = len(df.index) - df.apply(lambda column: sum(column[0:]==0) ,axis=0)
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
cols = df.columns.tolist()
print(cols)
```
```python
cols = list(df.columns)
print('", "'.join(cols))
```
### Statistics
```python
statistics = df.describe().loc[["mean", "std", "min", "25%", "50%", "75%", "max"]].round(2)
```
### get current directory
```python
import os
os.getcwd()
```
### change directory
```python
os.chdir("/path/")
```
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
* * *
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
