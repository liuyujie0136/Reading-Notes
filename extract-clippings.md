# Python Script for Extracting Clippings from Kindle

```python
#!/usr/bin/env python

# Usage: python extractClippings.py -i "My Clippings.txt" -b "路遥全集" -o "平凡的世界" -a "路遥" -t "2020-09 ~ 10"
# Latest update: 9/30/2024

import argparse
import re


def get_opt():
    group = argparse.ArgumentParser()

    group.add_argument(
        "-i", "--input", help="input clipping file's name", required=True
    )
    group.add_argument("-b", "--book", help="specified book's name", required=True)
    group.add_argument("-o", "--output", help="output file's name", required=True)
    group.add_argument("-a", "--author", help="author's name", required=True)
    group.add_argument("-t", "--time", help="time information", required=True)

    return group.parse_args()


opts = get_opt()
i = opts.input
b = opts.book
o = opts.output
a = opts.author
t = opts.time

file = open(i, "r", encoding="utf-8")
text = []
for line in file:
    if line != "\n" and line != "==========\n" and len(re.findall("^-", line)) == 0:
        text.append(line)
    if len(re.findall("Bookmark|书签", line)) != 0:
        text.append(line)

md = open("{}.md".format(o), "a", encoding="utf-8")
md.write("# {}\n> {}  \n> {}\n\n".format(o, a, t))

out = dict()
count = 1
for j in range(0, len(text), 2):
    if len(re.findall(b, text[j])) != 0:
        out[str(count)] = text[j + 1].replace(" ", "  \n")
        # this replacement is for poems only, but for bookmarks,
        # it may make some errors, just delete the error parts
        # as the bookmarks are not to be kept
        count += 1

for key, value in out.items():
    md.write("{}. {}".format(key, value))
```