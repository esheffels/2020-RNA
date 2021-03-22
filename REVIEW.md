# Code Review

## Code Formatting

### Python Notebook Code Formatting Usage

Cells in Python notebooks were formatted using [blackcellmagic](https://github.com/csurfer/blackcellmagic). blackcellmagic implements [black](https://github.com/psf/black), an uncompromising Python code formatter with a focus on standardization and readability.

To run blackcellmagic:

1. install blackcellmagic by opening a terminal and running `pip install blackcellmagic`
2. in a given Python notebook, insert a cell at the top with one line, `%load_ext blackcellmagic`, and run it
3. in any cell within that notebook, insert `%%black` as the first line of the cell, and run it - blackcellmagic will format the code in the cell; run the cell again execute it normally

The cell `%load_ext blackcellmagic` and individual `%%black` lines do not need to be retained (and are automatically removed when the cell with blackcellmagic is run), but are kept here for demonstration purposes.

### R Notebook Code Formatting

Alas, I could not find a Notebook magic cell or magic command for R formatting. So for the moment, you'll need to put up with my opinionated R code structuring. Specifically, I'm a strong advocate of conventions used in the [`tidyverse`](https://www.tidyverse.org/) group of packages, and make prominent use of the `%>%` pipe structure from the [`magrittr`](https://magrittr.tidyverse.org/) package in `tidyverse`. In short, it changes a nested function call like this (which calls from inside to outside):  

`order(rowMeans(counts(dds, normalized=TRUE)), decreasing=TRUE)[1:20]`  

to an unnested call like this (which calls from left to right, which I think is way more understandable):  

`counts(dds, normalized=TRUE) %>% rowMeans() %>% order(decreasing=TRUE) %>% .[1:20]`

## General Coding Suggestions

### Include More Documentation

This is a short comment, but generally, you should include much more exposition / text in your Jupyter Notebooks. That being said, you did indicate that this was an early draft, so it's totally understood that there wasn't much here yet. 

However, I would _strongly_ advocate that, even in your early drafts, you should over-explain every step. For example, in `featureCountprocessing-generic.ipynb`, I would expect a text cell before each of your defined functions describing what that function did. 

I ended up spending a lot of time figuring out what your code was trying to do. The Notebook format is specifically designed to allow exposition before code, and it's far better to over-write in Notebooks than to under-write.

### Where to Data Munge

You do a lot of data prep work in `featureCountprocessing-generic.ipynb`. Conceptually, I found that code is really just trying to do two things here:

1. Prepare the experimental design `.tsv` file
2. Prepare the featureCount count `.tsv` file

In short, I only used `featureCountprocessing-generic.ipynb` to generate your experimental design `.tsv` file, and then I implemented a simplified version of your featureCount count `.tsv` file munging in a new separate notebook, `differential-expression.ipynb`.

To address the former, I only used this part because I would normally expect an experimental design `.tsv` file to be "fully formed" when I start a differential expression analysis; that is, I don't expect to have to generate it on the fly. That's because, much of the time, experimental design `.tsv` files are manually generated in something like Excel to fit what DESeq2 wants as input. This makes sense in a "work smarter, not harder" way, because the data in this file is quite small, you _only really need to generate it once_, and it's specific to your research. I understood why you took a coding approach though, since you wanted to extract your experimental design from your file IDs. But this is a table that would be considered "raw input" into featureCounts.

For the latter, I moved the other data preparation steps into a new notebook because you should start a notebook with expected raw input (and any other meta-data necessary to bring your data through the analysis). Here, people reading your research will generally expect raw featureCounts table in an expected format, will expect your experimental design table in an expected format, and would expect any additional data to properly tie these inputs together.

### Avoid Function Dependecies Unless Absolutely Necessary

Generally speaking, functions are meant to be simple + reusable + independent code blocks. When functions are dependent on functions, it makes it difficult to trace code through them. It also makes it much harder to swap out one approach for another. This was particularly notable with `featureCountprocessing-generic.ipynb`, where it was hard to isolate the logic for generating the experimental design table. Overall, your sense for appropriate functions will develop more with time and practice, and from reading other people's code. Keep at it!

## DESeq2-specific Suggestions

### Don't Filter featureCounts Counts Before Feeding into DESeq2

Related to the content of `featureCountprocessing-generic.ipynb` was the fact that you filter your featureCounts count table by select gene sets prior to feeding it into DESeq2. Generally, we want to _take advantage of_ all the genes that were quantified in the experiment for shrinkage and count data normalization. 

This wasn't _that_ huge when it came to the quality assessment plots with the unsupervised clustering approach, but it would have big consequences on differential expression analysis. When you remove genes from the raw featureCounts table, you pretend like the only genes present in your genome were those genes, which is obviously far from reality. It also might accidentally lead you to using that `dds` object for differential expression analysis, which again, would produce misleading results.

### Use Gene IDs, Not Gene Names/Symbols

In your dataset I found that the gene names/symbols weren't unique. Because a gene name may be used on >1 distinct annotated regions, you can't simply remove rows with a repeated gene name. If you want to refer to gene names later for readability's sake (on a plot, for example), you can use the featureCounts table to translate gene IDs to gene names.

## More Reading

I adore the [DESeq2 vignette](https://www.bioconductor.org/packages/release/bioc/vignettes/DESeq2/inst/doc/DESeq2.html) (and I think you've already discovered it too). I also very much like [Harvard's differential expression workshop lessons with DESeq2](https://github.com/hbctraining/DGE_workshop/tree/master/lessons), which has a different conceputal presentation than the DESeq2 vignette that I think compliments it very nicely.