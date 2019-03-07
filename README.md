# bash_snippets

## Change filepaths

This showcases a loop over files from a `find` command and substring replacement with variables.

```bash
# rename filepaths v2.0
domain_old="old.loc"
domain_new="new.loc"
domain_paths=($( find . -name "$domain_old" ))
server_paths=($( find . -name "*.$domain_old" ))
for i in "${domain_paths[@]}"; do mv "$i" "${i/$domain_old/$domain_new}"; done
for i in "${server_paths[@]}"; do mv "$i" "${i/$domain_old/$domain_new}"; done
```

##  Change lines in many files

This showcases a loop over files from a recursive `grep` command (note the `-l` for just getting filepaths and `-i` to grab all cases) and multiple sed commands to replace different expected formats.

```bash
# Change to new domain 2.0
old_files=($( grep -r -l -iE 'old\.loc' . ))
for i in "${old_files[@]}"; do sed -e 's|old\.loc|new.loc|g' -e 's|OLD\.LOC|NEW.LOC|g' -i "$i"; done
```
