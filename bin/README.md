# "bin" directoy
This directory contains miscellaneous script utilities that are convenient when working with YAML and JSON files.
Each utility operates as a filter, reading the input from stdin and writing its output to stdout.

## `json2yaml`
Converts a JSON file to YAML.

    json2yaml <sample.json >sample.yaml
    
## `ppjson`
Pretty-prints a JSON file. Useful when JSON has had all whitespace removed.

    ppjson <sample.json | less
    
## `yaml2json`
Converts a YAML file to JSON.

    cat sample.yaml | yaml2json >sample.json
    
