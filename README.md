## Goal
Build a network intrusion detector, a predictive model capable of distinguishing between good and bad connections, also known as *intrusions* or *attacks*

## Data
[KDD Cup 1999 Data](https://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html)
> Trying to get this data returns a `403` error, so data is downloaded from here [Kaggle: KDD Cup 1999 Data](https://www.kaggle.com/datasets/galaxyh/kdd-cup-1999-data)

This database contains a standard set of data to be audited, which includes a
wide variety of intrusions simulated in a military network environment.

Attacks fall into four main categories:
- `DOS`: denial-of-service, e.g. syn flood;
- `R2L`: unauthorized access from a remote machine, e.g. guessing password;
- `U2R`:  unauthorized access to local superuser (root) privileges, e.g., various `buffer overflow` attacks;
- `probing`: surveillance and other probing, e.g., port scanning.

#### Common features
| Feature              | Description                                         | Type         |
| -------------------- | --------------------------------------------------- | ------------ |
| `hot`                | Number of "hot" indicators                          | `continuous` |
| `num_failed_logins`  | Number of failed login attempts                     | `continuous` |
| `logged_in`          | `1` if successfully logged in; `0` otherwise        | `symbolic`   |
| `num_compromised`    | Number of compromised conditions                    | `continuous` |
| `root_shell`         | `1` if root shell obtained; `0` otherwise           | `continuous` |
| `su_attempted`       | `1` if "su root" command attempted; `0` otherwise   | `continuous` |
| `num_root`           | Number of root accesses                             | `continuous` |
| `num_file_creations` | Number of file creation operations                  | `continuous` |
| `num_shells`         | Number of shell prompts                             | `continuous` |
| `num_access_files`   | Number of operations on access control files        | `continuous` |
| `num_outbound_cmds`  | Number of outbound commands in an FTP session       | `continuous` |
| `is_hot_login`       | `1` if login belongs to the hot list; `0` otherwise | `symbolic`   |
| `is_guest_login`     | `1` if login is a guest login; `0` otherwise        | `symbolic`   |

#### Content features within a connection suggested by domain knowledge
| Feature              | Description                                                                                 | Type         |
| -------------------- | ------------------------------------------------------------------------------------------- | ------------ |
| `count`              | Number of connections to the same host as the current connection in the past two seconds    | `continuous` |
| `serror_rate`        | `%` of connections that have `SYN` errors                                                   | `continuous` |
| `rerror_rate`        | `%` of connections that have `REJ` errors                                                   | `continuous` |
| `same_srv_rate`      | `%` of connections to the same service                                                      | `continuous` |
| `diff_srv_rate`      | `%` of connections to different services                                                    | `continuous` |
| `srv_count`          | Number of connections to the same service as the current connection in the past two seconds | `continuous` |
| `srv_serror_rate`    | `%` of connections to the same service that have `SYN` errors                               | `continuous` |
| `srv_rerror_rate`    | `%` of connections to the same service that have `REJ` errors                               | `continuous` |
| `srv_diff_host_rate` | `%` of connections to different hosts among those connected to the same service             | `continuous` |

#### Traffic features computed using a two-second time window
| Feature                       | Description                                                                          | Type         |
| ----------------------------- | ------------------------------------------------------------------------------------ | ------------ |
| `dst_host_count`              | Count of connections having the same destination host                                | `continuous` |
| `dst_host_srv_count`          | Count of connections having the same  destination host and service                   | `continuous` |
| `dst_host_same_srv_rate`      | `%` of connections to the same service                                               | `continuous` |
| `dst_host_diff_srv_rate`      | `%` of connections to different services                                             | `continuous` |
| `dst_host_same_src_port_rate` | `%` of connections to the same source port                                           | `continuous` |
| `dst_host_srv_diff_host_rate` | `%` of connections to different destination hosts among those using the same service | `continuous` |
| `dst_host_serror_rate`        | `%` of connections that have `SYN` errors                                            | `continuous` |
| `dst_host_srv_serror_rate`    | `%` of connections to the same service that have `SYN` errors                        | `continuous` |
| `dst_host_rerror_rate`        | `%` of connections that have `REJ` errors                                            | `continuous` |
| `dst_host_srv_rerror_rate`    | `%` of connections to the same service that have `REJ` errors                        | `continuous` |


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


