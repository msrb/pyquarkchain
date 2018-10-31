### TPS Competition Questionnaire

**Number of CPUs**

[How many logical CPUs does the machine have for running one cluster?]

36 vCPUs each machine, 65 machines per cluster (1 master, 64 slaves)

**Memory (GB)**

[How much memory does the machine have for running one cluster? For example, 16G.]

60 GiB, times 65

**Storage (GB)**

[Note down both the type and capacity of the storage on one machine. For example, SSD 1024G.]

200G, EBS

**Network**

[Comment on the network connecting clusters. For example, 1 Gbps LAN]

10Gbps (or higher, according to AWS)

**Machine Type (Optional)**

[If you are using public cloud service, note down the name of the provider and the machine type. For example, AWS EC2 m5.2xlarge.]

AWS EC2 c4.8xlarge


**Command Lines for Running Cluster**
```
# masters
screen -dm pypy3 pyquarkchain/quarkchain/cluster/master.py --cluster_config /tmp/cluster_config.json

# slaves (repeat for all servers, on different machines)
screen -dm pypy3 pyquarkchain/quarkchain/cluster/slave.py --cluster_config /tmp/cluster_config.json --node_id S0 ; screen -dm pypy3 pyquarkchain/quarkchain/cluster/slave.py --cluster_config /tmp/cluster_config.json --node_id S1 ;

# load test
curl -X POST --data '{"jsonrpc":"2.0","method":"createTransactions","params":{"numTxPerShard":10000, "xShardPercent":10},"id":0}' http://localhost:38491

```

**Peak TPS**

[Note down the highest TPS observed.]

40574.02


**Video URL**

[URL for the video showing how you produced the above TPS.]

https://www.youtube.com/watch?v=hpJfECyfUIo


**Output From `stats` Tool**
```
----------------------------------------------------------------------------------------------------
                                      QuarkChain Cluster Stats                                      
----------------------------------------------------------------------------------------------------
CPU:                36
Memory:             58 GB
IP:                 localhost
Shards:             1024
Servers:            128
Shard Interval:     10
Root Interval:      120
Syncing:            False
Mining:             True
Peers:              172.31.19.39:38291, 172.31.26.124:38291
----------------------------------------------------------------------------------------------------
Timestamp                     TPS   Pending tx  Confirmed tx       BPS      SBPS      ROOT       CPU
----------------------------------------------------------------------------------------------------
2018-10-31 17:49:21          0.00         4876       4868915    111.48      0.00        14      2.87
2018-10-31 17:49:31       4157.20       181836       5118347    108.43      0.00        14      0.67
2018-10-31 17:49:42       9355.28       367047       5430232    104.12      0.00        14      0.68
2018-10-31 17:49:52      14802.12       532710       5757042     98.87      0.00        14      0.83
2018-10-31 17:50:02      20636.05       666363       6107078     93.92      0.00        14      1.24
2018-10-31 17:50:12      26232.82       798383       6442884     88.50      0.00        14      0.94
2018-10-31 17:50:22      32155.75       925075       6798260     82.90      0.00        14      0.98
2018-10-31 17:50:32      37638.53      1029832       7161405     78.25      0.00        14      0.73
2018-10-31 17:50:42      39900.63      1107506       7479846     76.62      0.00        14      0.64
2018-10-31 17:50:52      40574.02      1215872       7784482     75.48      0.00        14      0.61
2018-10-31 17:51:02      40557.85      1334249       8093492     73.92      0.00        14      0.56
2018-10-31 17:51:12      40251.88      1432976       8355068     72.63      0.00        14      0.54
2018-10-31 17:51:23      39379.73      1554724       8672800     70.38      0.00        14      0.51
2018-10-31 17:51:33      38223.05      1645600       8957993     68.00      0.00        14      0.49
2018-10-31 17:51:43      37313.28      1748993       9246272     66.10      0.00        14      0.50
2018-10-31 17:51:53      36511.00      1844575       9517686     64.53      0.00        14      0.49
2018-10-31 17:52:03      35482.05      1946225       9780608     62.58      0.00        14      0.49
2018-10-31 17:52:13      34461.53      2060903      10065789     60.70      0.00        14      0.55
2018-10-31 17:52:23      33649.63      2148074      10322597     59.22      0.00        14      0.55
2018-10-31 17:52:33      32709.95      2236027      10605665     57.50      0.00        14      0.56
2018-10-31 17:52:43      32113.60      2341090      10907044     56.42      0.00        14      1.05
2018-10-31 17:52:54      31592.23      2407753      11178818     55.48      0.00        14      0.64
2018-10-31 17:53:04      31014.82      2367514      11531642     54.45      0.00        14      0.63
2018-10-31 17:53:21      33509.30      1875877      12191950     58.80      0.00        15      2.04
2018-10-31 17:53:31      34139.90      1737637      12348794     59.90      0.00        15      0.29
2018-10-31 17:53:42      34139.90      1737637      12348794     59.90      0.00        15      0.96
2018-10-31 17:53:52      34139.90      1737637      12348794     59.90      0.00        15      0.09
2018-10-31 17:54:02      34139.90      1737637      12348794     59.90      0.00        15      0.09
2018-10-31 17:54:12      34139.90      1737637      12348794     59.90      0.00        15      0.04
2018-10-31 17:54:22      34139.90      1737637      12348794     59.90      0.00        15      0.09
2018-10-31 17:54:32      34139.90      1737637      12348794     59.90      0.00        15      0.05
2018-10-31 17:54:42      34139.90      1737637      12348794     59.90      0.00        15      0.09
2018-10-31 17:54:52      34139.90      1737637      12348794     59.90      0.00        15      0.04
2018-10-31 17:55:02      34139.90      1737637      12348794     59.90      0.00        15      0.09
2018-10-31 17:55:12      34139.90      1736852      12349933     59.90      0.00        15      0.05
2018-10-31 17:55:22      34139.90      1736852      12349933     59.90      0.00        15      0.09
2018-10-31 17:55:32      34139.90      1736852      12349933     59.90      0.00        15      0.04
2018-10-31 17:55:43      34139.93      1735711      12351074     59.90      0.00        15      0.09
2018-10-31 17:55:53      34140.12      1731145      12355640     59.90      0.00        15      0.06
2018-10-31 17:56:03      34159.15      1729435      12357350     59.93      0.00        15      0.08
2018-10-31 17:56:13      29100.20      1567000      12520591     51.07      0.00        15      0.24
2018-10-31 17:56:23      15188.28      1166224      12925459     26.83      0.00        15      0.48
2018-10-31 17:56:33      11716.70       706963      13390554     22.30      0.00        15      0.50
2018-10-31 17:56:43      16363.18       271935      13830614     37.32      0.00        15      0.46
2018-10-31 17:56:53      19138.43        71216      14033338     57.63      0.00        15      0.34
2018-10-31 17:57:03      19345.40        18400      14086625     76.07      0.00        15      0.55
2018-10-31 17:57:13      19428.22         1702      14103423     93.65      0.00        15      0.31
2018-10-31 17:57:23      16467.48          505      14104620    105.17      0.00        15      0.38
2018-10-31 17:57:34      11499.10            0      14105125    111.52      0.00        15      0.32
2018-10-31 17:57:44       6711.62            0      14105125    113.55      0.00        15      0.23
2018-10-31 17:57:54       3253.82            0      14105125    113.87      0.00        15      0.30
2018-10-31 17:58:04       1361.53            0      14105125    113.90      0.00        15      0.28
2018-10-31 17:58:14        518.00            0      14105125    113.80      0.00        15      0.28
2018-10-31 17:58:24        220.15            0      14105125    112.72      0.00        15      0.25
2018-10-31 17:58:34         83.57            0      14105125    112.45      0.00        15      0.30
2018-10-31 17:58:44         26.82            0      14105125    113.08      0.00        15      0.29
2018-10-31 17:58:54         26.82            0      14105125    113.37      0.00        15      0.30
2018-10-31 17:59:04          7.35            0      14105125    111.97      0.00        15      0.30
2018-10-31 17:59:14          0.00            0      14105125    112.28      0.00        15      0.28
```

**Additional Comment**

[If you have special setup, e.g., running a single cluster over multiple machines, the above questionnaire might not fit. Note down
whatever you want us to know here to help evaluate the result.]

Each cluster consisted of 65 EC2 c4.8xlarge nodes. 1 node acting as a master for the cluster and 64 nodes running slave servers. The decision to go with c4.8xlarge was a bad one as I couldn't utilize the vast majority of CPUs that were available in the cluster (machines would run out of memory real quick with higher number of slaves/shards). I *think* using more smaller instances, with less CPU and more RAM could yield much better results. However, there is a limit on number of memory-optimized instances that I can create in my AWS account, and the limit is quite low. So I decided to go with the less-than-optimal c4.8xlarge instances.

You can find all cluster configs in the [tps](tps/) directory.

Note I had to rebuild RocksDB from sources as I was getting an error (`Illegal instruction (core dumped)`) on c4.8xlarge instances. The new AMI is `ami-0796d033ea5e1b079`. It should be publicly available in AWS so feel free to check it out ;)
