# Some useful Shell-command, just in case of oblivous.
1. For processing a log file in batching, you may need to use commands like grep, zgrep, cat, head, tail, awk.
1.1 Accumuate a column($1 represent the first column) in a file.
```bash
awk '{sum+=$1};{print sum}' log 
```
or to only print out the final result:

```bash
awk '{sum+};END{print sum}' log
```
Above commands all assume that each comlumn is divided by the space or tab (" ","\t").

1.2
you can specify a character to divide each column by -F:
```bash
awk -F "," '{print $1}' log 
```
will divide each column by ','.

1.3 Find the maximal or minumal value inside a column of a log file.
```bash
awk -v max=0 -F "," '{if($1>max){want=$1; max=$1}}END{print want} ' log
```
will print out the maximal value in the first column of the log.

```bash
awk -v min=0 -F "," '{if($1<min){want=$1; min=$1}}END{print want} ' log
```
will print out the minumal value.
