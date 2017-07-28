# dependency_stags

Extract dependency tree supertags from CoNLL data. The supertags are the ones described in [Ouchi et al., 2014](http://www.anthology.aclweb.org/E/E14/E14-4030.pdf) and [Foth et al., 2006](http://anthology.aclweb.org/P/P06/P06-1.pdf#page=329).

## Requirements

python 2.7

## Data

The extractor expects a file or list of files in CoNLL-09 format, but any CoNLL file will work as long as there is a column for word index, head, dependency relation, and part of speech. To use a different CoNLL format, open `extract.py` and edit the `conll_line_to_dict` function to match your format. Specifically, edit lines 19 and 20:
```python
    fields = [(0, 'idx', int), (4, 'pos', str),
              (8, 'head', int), (10, 'deprel', str)]    
```
so that the first element in each tuple (the column index) matches the column index in your data.

You also need to edit `arg_list` in `get_model2_stag`, which lists the arguments that are considered to be required for forming model2 supertags. According to Ouchi et al., these are SUBJ (subject), OBJ (object), PRD (predicative complement), and VC (verb chain). You need to change this to match your dependency formalism. 

## Supertag models

This code extracts supertags models 1 and 2 from Outhi et al. (2014) and also the model from Foth et al. (2006), which is numbered here as model 0. See those papers for details.

## Usage

```
python extract.py model_number file1.txt [file2.txt ...]
```
