# PDF-to-Text
A python terminal program to convert PDF files into TXT


This is a simple program.

Llamafile is a powerful tool for AI, and works out of the box with a terminal UI

It can read a txt document (but not a pdf)

The solution?  We first convert the document in the terminal, and then we load it into Llamafile


### Requirements
```
pip install easygui pypdf pyinstaller
```

### Convert the python file in a terminal based .exe application
```bash
pyinstaller --onefile pdf_extractor.py
```

### The simple python code
````python
# Created by Fabio Matricardi 06 April 2025
# fabio.matricardi@gmail.com
# https://github.com/fabiomatricardi

import os
import pypdf
from easygui import fileopenbox

current_directory = os.getcwd()

def writehistory(filename,text):
    with open(filename, 'x', encoding='utf-8') as f:
        f.write(text)
        f.write('\n')
    f.close()

pdffile = fileopenbox(msg='Pick your PDF', default='*.pdf')
try:
    reader = pypdf.PdfReader(pdffile)
    text = ""
    page_count = len(reader.pages)
    for i, page in enumerate(reader.pages):
        page_text = page.extract_text()
        if page_text: text += page_text + "\n"
    a = text.strip()
    textfile = a.replace('\n\n','')
    textfilename = f'{pdffile.split('\\')[-1][:-3]}txt'
    print('Creating text file...')
    writehistory(textfilename,textfile)
    print(f"Parsed from PDF {page_count} pages of text into file {textfilename}")
except Exception as e:
    print(f"Error reading PDF {pdffile}: {e}")
```
