# wilson52-training-lines
Parsed and confirmed hocr lines from the Wilson 1852-1853 Business Directory
##Overview
These files are outputs from ongoing efforts to extract address and business data from [*Wilson's Business Directory of New-York City* (1852)](https://digitalcollections.nypl.org/items/de3c45b0-a30b-0131-2a1e-58d385a7b928) that have been scanned and made available online by the New York Public Library. They consist of confirmed word tokens from the directory grouped by line, totalling 11,066 lines (out of 32,000+ entries in the directory), and their associated [hocr bounding boxes](https://kba.github.io/hocr-spec/1.2/). The underlying OCR hocr outputs are the files produced by NYPL using Tesseract and [hosted here] (https://github.com/hadro/Wilson-Business-Directories).

The hocr lines produced by Tesseract were compared against a second OCR output produced by ABBYY Finereader (using in-built pattern matching, no training) and those lines that matched character-for-character across the entire line (using Levenshtein ratio calculations) were included in these files along with their bounding box information. Ongoing work on the ABBYY outputs has also produced corrected versions of all street addresses and identification of last and first names in the directory. The files here include these identifications in case they prove useful for parsing other address entries.

##Format

The data are provided in two formats, csv and json, with the following variables:

**id**: A unique numerical identifier for each entry token.

**filename**: The filename of the associated hocr file generated in Tesseract by NYPL available [here](https://github.com/hadro/Wilson-Business-Directories).

**page**: The page number of the original directory "proper," i.e. the alphabetized listings that follow the advertisements and index. Note that the original restarts its page numbers at the start of the directory proper, i.e. at letter "A" and continues this sequence to page 343. Because these files include only lines that are confirmed, not all page numbers will be represented here.

**column**: The column number (1 or 2) that the word appears.

**linenum**: The hocr line designation (unique to each page) of each line. Given in format as a string: line_1_1 etc.

**entrynum**: A unique identifying number across the entire dataset for each line of text. Grouping words by entrynum will enable reconstruction of lines (whereas **linenum** will not because unique to a given page only).

**linebb**: The hocr bounding box coordinates of the line. See the [hocr documentation](https://kba.github.io/hocr-spec/1.2/) for details. Given as a series of four numbers separated by a single whitespace.

**wordnum**: An hocr designation (unique to each page) of each word token. Given in format as a string: word_1_1 etc.

**wordbb**: The hocr bounding box coordinates of the word token, given as a series of four numbers separated by a single whitespace.

**value**: The string returned by the Tesseract output.

**abbyyentry**: The string returned by the ABBYY Finereader output at that same line and word location.

**valuetype**: A description of the type of entity represented by the token. The entries are:

 - lastname: The **value** is a surname.
 
 - firstname: The **value** is a given name. Note that initials (e.g. J. L. Jones) are excluded from this labeling.
 
 - addressnum: The **value** is a an address number (e.g. 4, 12, 14 1/2, 16).
 
 - street: The **value** is a street name.
 
 - bldgsection: The **value** is a sub-designation of the street address. Options are 'r.' (rear) and 'cor.' (corner).

 - unknown: The type of **value** is unknown. In most cases, these can be discerned by regular pattern matching (e.g. 'jr.' fo r 'junior', 'and' for the conjunction 'and', '&', etc.
 
**standardvalue**: The matched and human-corrected (in the case of street addresses) standardized version of the **value**. These are given in title case, with all abbreviations extended (st. >> Street, av. >> Avenue). If a **standardvalue** was given, it will match at a Levenshtein distance of 0 or 1 to the Tesseract hocr token (in the case of names), and be matched to the full standard street address (in the case of street names and numbers). 

There are multiple addresses for some entries in the directory. In those cases, the full standardized entry of the most closely  matching address, not necessarily the first, is given.



##Process

```
code
```

