# Bash Script for Processing OCR Outputs

```bash
#!/bin/bash

# Usage: bash ocr-processing.sh 1 tmp.txt > tmp.out
# Note: the first arg: "1" for common files , and "2" for poems especially

if [ $1 -eq 1 ]
then
    cat $2 | sed 's/[a-z]//g; s/[A-Z]//g; s/[0-9]//g; s/ //g; s/,/，/g; s/;/；/g; s/:/：/g; s/?/？/g; s/!/！/g'
elif [ $1 -eq 2 ]
then
    cat $2 | sed 's/[a-z]//g; s/[A-Z]//g; s/[0-9]//g; s/ /  \n/g; s/,/，/g; s/;/；/g; s/:/：/g; s/?/？/g; s/!/！/g'
fi

exit 0
```