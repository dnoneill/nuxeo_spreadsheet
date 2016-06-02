Python scripts for processing and migrating data into Nuxeo

# Prerequisites
[see the wiki for this repo](https://github.com/ucldc/nuxeo_spreadsheet/wiki)

# Using `csv2dict`
`csv2dict` constitutes a set of prototype Python scripts, which can be used to import tab-delimited spreadsheet metadata into  Nuxeo. Note that CSV-based spreadsheets are not supported ("csv" is a misnomer).

1) Once your `.pynuxrc` file is configured, upload your content files into a Project Folder in Nuxeo.  Import the files through the Nuxeo UI, or use the <a href="https://registry.cdlib.org/documentation/docs/dams/bulk-import/">bulk import options</a>.

2) Next, generate a list of directory paths for the files in that Project Folder.  Make sure you are in your python environment (e.g., venv) and run this command. 
```
nxls /asset-library/UCX/Project_folder
```

If you're using miniconda within Windows, here's an overview of the process:

* Open the Command Prompt from the Start menu
* Activate your python environment.  In this example, we're activating a python environment named "venv": `activate venv`
* Run the command: `nxls /asset-library/UCX/Project_folder`

3) Use the <a href="https://docs.google.com/spreadsheets/d/1JFiLA2eE6O2KDtSl3nHGpNU7zGP8Sk4p60GqOZtnUoM/edit#gid=0">Nuxeo CSV Import Template</a> to format your metadata records. The first tab comprises the template; the second tab provides an example for reference purposes.  Note with the following considerations:

* The column headings need to have the exact same headings as the Nuxeo metadata elements. You can double-check the headings by reviewing the source `meta_from_csv.py` file in GitHub.

* Each row should contain metadata for either a simple object, or the parent-level record for a complex object.  

* <b>File Path</b> (color-coded in red) is required for each row; additionally, either <b>Title</b>, <b>Type</b>, <b>Copyright Status</b>, and/or <b>Copyright Statement</b> is required, if and when the objects will be published in Calisphere. For additional information on the metadata requirements, see the <a href="https://registry.cdlib.org/documentation/docs/dams/metadata-model/">Nuxeo user guide</a>

* The <b>File Path</b> cell should contain the exact file directory path to the content file in Nuxeo, to be associated with the metadata record (e.g., "/asset-library/UCOP/nuxeo_tab_import_demo/ucm_li_1998_009_i.jpg").

* If using Google Sheets directly to create your metadata records, note that some of the fields have validation rules.  These fields are keyed to controlled vocabularies established in Nuxeo.

* Once you've completed the process of creating metadata records using the template, save a copy as a tab-delimited file.

![screen shot 2016-06-01 at 5 23 53 pm](https://cloud.githubusercontent.com/assets/227374/15734242/789b2380-2842-11e6-9427-a39f64eed608.png)

If using Google Sheets, download as tab seperated value:

<img width="642" alt="screen shot 2016-06-01 at 9 59 58 pm" src="https://cloud.githubusercontent.com/assets/227374/15734442/9421a0c8-2844-11e6-8179-27e4397e8c4d.png">
 

4) Load with `meta_from_csv.py`. This process will convert the metadata from the CSV file into Python dict outputs, and call pynux to import the Python dict outputs directly into Nuxeo.

```
usage: meta_from_csv.py [-h] --datafile DATAFILE [--loglevel LOGLEVEL]
                        [--rcfile RCFILE]

optional arguments:
  -h, --help           show this help message and exit
  --datafile DATAFILE  CSV data input file -- required

common options for pynux commands:
  --loglevel LOGLEVEL  CRITICAL ERROR WARNING INFO DEBUG NOTSET, default is
                       ERROR
  --rcfile RCFILE      path to ConfigParser compatible ini file
```

Note for Windows: you may need to run `python meta_from_csv.py ...`
or edit the shebang. If you're using miniconda within Windows, here's an overview of the process:

* Open the Command Prompt from the Start menu
* Activate your python environment.  In this example, we're activating a python environment named "venv": `activate venv`
* Go to the csv2dict directory on your computer, e.g.: `cd C:\Users\yourname\nuxeo_spreadsheet\csv2dict`
* Run the command.  In this example, the DATAFILE is the location of a tab-delimited file (named "tab-delimited-metadata.txt") that's on our Desktop. `python meta_from_csv.py --datafile C:\Users\yourname\Desktop\tab-delimited-metadata.txt`


## `mets_example`
Sample code for loading METS into Nuxeo
