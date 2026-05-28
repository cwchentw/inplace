# inplace 🚀

A lightweight command-line tool to edit your text data efficiently in-place! Ideal for streamlined data cleaning and pre-processing pipelines.

## ⚠️ Warning

`inplace` permanently modifies your files **IN-PLACE**. Always back up your critical data before running execution commands.

## Installation

Make the script executable and copy it to your local environment path:

```shell
chmod +x inplace
cp -p inplace ~/bin/
```

## Usage & Data Cleaning Workflow

When dealing with complex CSV files, embedded commas within quotes (like dates or currency) often break standard column splitting. Here is how `inplace` helps you clean and extract data step-by-step.

### 1. Back up your original dataset

```shell
cp VT.csv VT_orig.csv
```

### 2. Clean up embedded commas

Use `inplace` alongside `perl` to pre-process messy columns before splitting:

```shell
# Convert date format inside quotes: "May 28, 2026" -> May-28-2026
inplace perl -pe 's/"([A-Za-z]+) ([0-9]+), ([0-9]+)"/$1-$2-$3/g' VT.csv

# Remove thousands separators inside quotes: "1,234,567" -> 1234567
inplace perl -pe 's/"([0-9]+),([0-9]+),([0-9]+)"/$1$2$3/g' VT.csv
```

### 3. Extract final columns safely

Once the conflicting commas are removed, extract your target columns into a new clean dataset:

```shell
awk 'BEGIN { FS=","; OFS="," } { print $1, $5, $6 }' VT.csv > VT_extracted.csv
```

## License

Copyright (c) 2026 ByteBard. Licensed under the [MIT License](LICENSE).
