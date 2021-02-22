# Bash Script for Processing OCR Outputs

```bash
#!/bin/bash

# Usage: bash ocr-processing.sh 2 tmp.txt > out.md
# Note the First Arg: "1" for common files , and "2" for poems especially

if [ $1 -eq 1 ]
then
    cat $2 | sed 's/[a-z]//g; s/[A-Z]//g; s/[0-9]//g; s/ //g; s/,/，/g; s/;/；/g; s/:/：/g; s/?/？/g; s/!/！/g'
elif [ $1 -eq 2 ]
then
    cat $2 | sed 's/[a-z]//g; s/[A-Z]//g; s/[0-9]//g; s/ /  \n/g; s/,/，/g; s/;/；/g; s/:/：/g; s/?/？/g; s/!/！/g; s/(/\n## /g; s/)/\n/g; s/</\n### /g; s/>/\n/g'
fi

exit 0
```