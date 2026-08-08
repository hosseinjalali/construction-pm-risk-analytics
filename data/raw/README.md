# Raw data

This folder is where the two source CSVs go. They are **not committed to this
repository** (see `.gitignore`) to keep the repo lightweight and to respect the
dataset's original distribution on Kaggle.

## Download

1. Go to the Kaggle dataset page:
   https://www.kaggle.com/datasets/claytonmiller/construction-and-project-management-example-data
2. Download the two files and place them here, unchanged:
   - `Construction_Data_PM_Forms_All_Projects.csv`
   - `Construction_Data_PM_Tasks_All_Projects.csv`

Alternatively, with the Kaggle CLI configured (`pip install kaggle` + API token):

```bash
kaggle datasets download -d claytonmiller/construction-and-project-management-example-data -p data/raw --unzip
```

Once both files are in place, run the notebooks in order starting from
`notebooks/01_data_exploration.ipynb`. See the top-level `README.md` for the full
walkthrough of what each notebook does and why.
