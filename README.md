## Goal
Build a network intrusion detector, a predictive model capable of distinguishing between good and bad connections, also known as *intrusions* or *attacks*

## Data
[KDD Cup 1999 Data](https://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html)
This database contains a standard set of data to be audited, which includes a
wide variety of intrusions simulated in a military network environment.

> why is the below section in the task description???
A connection is a sequence of TCP packets 
- starting and ending at defined times, between which data rows
- to and from a source IP address
- to a target IP address under some well defined protocol.

Each connection is labeled as either:
- normal
- attack, with exactly one specific attack type.

#### Data set used for each elements
- Train: kddcup.data_10_percent.gz
- Test Unlabeled: kddcup.testdata.unlabeled_10_percent.gz
- Test target labels: corrected.gz


