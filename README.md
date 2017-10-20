# vertica-query-paste
Shell script for quick and easy exporting of CSV from Vertica database.

## Usage
Copy a query from your SQL client in MacOS or X window system. Run the script. Your CSV will pop out of STDOUT.

Connection parameters are taken out of `vsql` environment variables, with default `vsql` defaults.

```bash
vertica-query-paste > data.csv
```

If you have `pv` (and you should), you can make in nicer:

```bash
vertica-query-paste | pv -l > data.csv
```

If you have two environments, production and test, you can add `_env` to your vsql variable names to set up an alternative. For example, you could have `VSQL_HOST=192.168.0.1` and `VSQL_HOST_test=127.0.0.1`. Then you can do:

```bash
vertica-query-paste | pv -l > data.csv  # production env at 192.168.0.1
vertica-query-paste test | pv -l > test_data.csv  # from local test env
```

You can also pass an alternative delimiter as a second parameter (the default is `,`):

```bash
vertica-query-paste '' ';' | pv -l > data_eastern_european.csv
```

I usually set up an alias script for my particular format of CSV (`;` as delimiter):

```bash
#!/bin/bash
# at ~/bin/vqp
vertica-query-paste $1 ';' | pv -l
```
