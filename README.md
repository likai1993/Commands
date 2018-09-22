## Here are some useful Shell commands. Take some notes just in case of oblivious. 
### 1. For processing a log file in batching, you may need to use commands like grep, zgrep, cat, head, tail, awk.

#### 1.1 Accumuate a column($1 represents the first column) in a file.
```bash
awk '{sum+=$1};{print sum}' log 
 ```
 will print out the 'sum' at each step.

```bash
awk '{sum+};END{print sum}' log
```
will only print out the final step.


#### 1.2 Above commands all assume to divided each column by \space or \tab. You can specify it by -F:
```bash
awk -F "," '{print $1}' log 
```
will divide each column by ','.

#### 1.3 Find the maximal or minumal value inside a column of a log file.
```bash
awk -v max=0 -F "," '{if($1>max){want=$1; max=$1}}END{print want} ' log
```
will print out the maximal value in the first column of the log.

```bash
awk -v min=0 -F "," '{if($1<min){want=$1; min=$1}}END{print want} ' log
```
will print out the minumal value.

### 2. Sometime you may need to kill a set of processes in a time, you can use xargs.
```bash
ps -ef |grep 'nginx' |awk '{print $2}' |xargs kill -9
```
will kill all the processes whose name contains 'nginx'.
