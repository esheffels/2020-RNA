# Code Review

## Python Notebook Code Formatting Usage

Cells in Python notebooks were formatted using (blackcellmagic)[https://github.com/csurfer/blackcellmagic]. blackcellmagic implements (black)[https://github.com/psf/black], an uncompromising Python code formatter with a focus on standardization and readability.

To run blackcellmagic:

1. install blackcellmagic by opening a terminal and running `pip install blackcellmagic`
2. in a given Python notebook, insert a cell at the top with one line, `%load_ext blackcellmagic`, and run it
3. in any cell within that notebook, insert `%%black` as the first line of the cell, and run it - blackcellmagic will format the code in the cell; run the cell again execute it normally

The cell `%load_ext blackcellmagic` and individual `%%black` lines do not need to be retained (and are automatically removed when the cell with blackcellmagic is run), but are kept here for demonstration purposes.

