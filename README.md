# SciHub to PDF(Beta)

Many thanks to [bibcure](https://github.com/bibcure) for the original repository: https://github.com/bibcure/scihub2pdf

## :no_entry: Disclaimer :no_entry:
**I am not responsible for the illegitimate use of this tool. For example, the download of non-open-access papers or even those if this method is not allowed by the editors.**


## Install and Config
```bash
python install -r requirements.txt
```

If you want  to download files from scihub you will need to 
1. download [chromwdriver](https://chromedriver.chromium.org/), make sure the version same with the Google Chrome browser you used.
1. modify `driver_path` value in the `config.py`

The given title will be used as the pdf filename. Please note that the character ':' will be replaced by the
 character " -" because of the restricts of filename in Windows.

You can modify those configs in `config.py` if needed


## Features and How to Use

Given a bibtex file
```
$ scihub2pdf -i input.bib
```

Given a DOI number...
```
$ scihub2pdf 10.1038/s41524-017-0032-0
```

Given a title...
```
$ scihub2pdf --title "An useful paper"
```

Arxiv...
```
$ scihub2pdf arxiv:0901.2686
$ scihub2pdf --title arxiv:Periodic table for topological insulators
```

Location folder as argument
```
$ scihub2pdf -i input.bib -l somefoler/
```

Use libgen instead sci-hub

```
$ scihub2pdf -i input.bib --uselibgen
```

## Sci-hub:

- Stable
- Annoying CAPTCHA
- Fast


## Libgen

- Unstalbe
- No CAPTCHA
- Slow

## Download from list of items

Given a text file like

```
10.1038/s41524-017-0032-0
10.1063/1.3149495
.....
```
download all pdf's
```
$ scihub2pdf -i dois.txt --txt
```
Given a text file like

```
Some Title 1
Some Title 2
.....
```
download all pdf's
```
$ scihub2pdf -i titles.txt --txt --title
```
Given a text file like

```
arXiv:1708.06891
arXiv:1708.06071
arXiv:1708.05948
.....
```
download all pdf's
```
$ scihub2pdf -i arxiv_ids.txt --txt
```

# Notes
- when get arxiv items by title, we want to use the first one directly instead of asking user to choose one by promoting an input, 
    which will hang the download process. See the code below `title2bib\crossref.py`:
    
    ```python
    def get_from_title(title, get_first=False):
        # ...
    
        if r.status_code == 200 and len(items) > 0:
            items = sort_items_by_title(items, title)
            # use the first item directly
            found = True
            item = items[0]
  
            # if get_first:
            #     found = True
            #     item = items[0]
            # else:
            #    found, item = ask_which_is(title, items)
    
        # ...
    ```
