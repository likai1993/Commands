## Here are some great useful commands to conduct the statistic analysis.
### 1. Process lines of a file in batch and apply mathematical computation.
#### 1.1 Accumuate by a column($1 represents the first column).
```bash
awk '{sum+=$1};{print sum}' log 
 ```
 will print out the `sum` at each step.

```bash
awk '{sum+};END{print sum}' log
```
will only print out the final step.


#### 1.2 Above commands divide each column by `\space` or `\tab` by default. You can customize the division character by `-F`:
```bash
awk -F "," '{print $1}' log 
```
will divide each column by `,` and print out the first column.

#### 1.3 Find the maximal or minimal value inside a column of a file.
```bash
awk 'BEGIN{first=1;} {if (first) { max = $1; first = 0; next;} if (max < $1) max=$1;} END {print max}' log
```
will print out the maximal value in the first column of the log.

```bash
awk 'BEGIN{first=1;} {if (first) { min = $1; first = 0; next;} if (min > $1) min=$1;} END {print min}' log
```
will print out the minimal value.

```bash
awk 'BEGIN{first=1;} {if (first) { max = min = $1; first = 0; next;} if (max < $1) max=$1; if (min > $2) min=$2; } END { print min,max}' log
```
will print put both minimal and maximal value.

### 2. To kill a set of processes in a time, you can use `xargs`.
```bash
ps -ef |grep 'nginx' |awk '{print $2}' |xargs kill -9
```
will kill all the processes whose name contains `nginx`.

### 3. To install the python package to a specific python environment.
```bash
sudo python2.7 -m pip install pycoin
```
