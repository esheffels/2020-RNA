# Code Review

## Python Notebook Code Formatting

Cells in Python notebooks were formatted using (blackcellmagic)[]. blackcellmagic implements black, an uncompromising Python code formatter with a focus on standardization and readability.

To run blackcellmagic:

1. install blackcellmagic by opening a terminal and running `pip install blackcellmagic`
2. in a given Python notebook, insert a cell at the top with one line, `%load_ext blackcellmagic`, and run it
3. in any cell within that notebook, insert ``

The cell `%load_ext blackcellmagic` and individual `%%black` lines do not need to be retained, but are kept here for demonstration purposes.