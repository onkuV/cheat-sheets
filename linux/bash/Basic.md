to rename all files/folder in a directory with 'space( )' to 'underscore '__'
```bash
for file in *; do mv "$file" `echo $file | tr ' ' '_'` ; done
```
To read each line and pass them as variable
```bash
while read envs; do

    echo "$envs"

done <texts.txt
```
