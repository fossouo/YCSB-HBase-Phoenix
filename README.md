# Performance Test YCSB : 

Install Maven using the below settings : 

`https://gist.github.com/fossouo/75da8b09125b214c63a4284a1c30cc40`

Java 1.8 & HBase conf : 

`export HBASE_CONF_DIR=/etc/hbase/conf`   
`export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el7_7.x86_64`   
`export PATH=$PATH:/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el7_7.x86_64/bin`   

Copy hbase-site.xml in each project folder :  

cp /etc/hbase/conf/hbase-site.xml /root/YCSB-HBase-Phoenix/asynchbase/src/test/resources/hbase-site.xml   
cp /etc/hbase/conf/hbase-site.xml /root/YCSB-HBase-Phoenix/asynchbase/target/test-classes/hbase-site.xml   
cp /etc/hbase/conf/hbase-site.xml /root/YCSB-HBase-Phoenix/hbase10/src/test/resources/hbase-site.xml   
cp /etc/hbase/conf/hbase-site.xml /root/YCSB-HBase-Phoenix/hbase12/src/test/resources/hbase-site.xml   
cp /etc/hbase/conf/hbase-site.xml /root/YCSB-HBase-Phoenix/hbase14/src/test/resources/hbase-site.xml   
cp /etc/hbase/conf/hbase-site.xml /root/YCSB-HBase-Phoenix/hbase20/src/test/resources/hbase-site.xml   


If kerberized cluster load your keytab. 



create table usertable(YCSB_KEY VARCHAR(255) NOT NULL PRIMARY KEY, FIELD0 VARCHAR, FIELD1 VARCHAR, FIELD2 VARCHAR, FIELD3 VARCHAR,FIELD4 VARCHAR, FIELD5 VARCHAR,FIELD6 VARCHAR, FIELD7 VARCHAR,FIELD8 VARCHAR, FIELD9 VARCHAR) SALT_BUCKETS=8;  

Then number of salt bucket varies according to your cluster size.  

create index idx1 on usertable(field0, field1) include(field8, field9);  
create index idx2 on usertable(field2, field3) include(field8, field9);  

phoenix.properties

`db.driver=org.apache.phoenix.jdbc.PhoenixDriver  
db.url=jdbc:phoenix:dfossouoenelamis-2.vpc.cloudera.com:2181:/hbase  
jdbc.autocommit=false  
db.batchsize=1000`


Launch Parameter :

`/usr/java/jdk1.8.0_162-cloudera/bin/java -cp /root/YCSB-master/jdbc/conf:/root/YCSB-master/jdbc/target/jdbc-binding-0.18.0-SNAPSHOT.jar:/root/.m2/repository/org/apache/geronimo/specs/geronimo-jta_1.1_spec/1.1.1/geronimo-jta_1.1_spec-1.1.1.jar:/root/.m2/repository/org/apache/htrace/htrace-core4/4.1.0-incubating/htrace-core4-4.1.0-incubating.jar:/root/.m2/repository/net/sourceforge/serp/serp/1.13.1/serp-1.13.1.jar:/root/.m2/repository/org/hdrhistogram/HdrHistogram/2.1.4/HdrHistogram-2.1.4.jar:/root/.m2/repository/org/apache/openjpa/openjpa-jdbc/2.1.1/openjpa-jdbc-2.1.1.jar:/root/.m2/repository/org/apache/geronimo/specs/geronimo-jms_1.1_spec/1.1.1/geronimo-jms_1.1_spec-1.1.1.jar:/root/.m2/repository/org/apache/openjpa/openjpa-kernel/2.1.1/openjpa-kernel-2.1.1.jar:/root/.m2/repository/org/codehaus/jackson/jackson-core-asl/1.9.4/jackson-core-asl-1.9.4.jar:/root/YCSB-master/core/target/core-0.18.0-SNAPSHOT.jar:/root/.m2/repository/commons-collections/commons-collections/3.2.1/commons-collections-3.2.1.jar:/root/.m2/repository/commons-lang/commons-lang/2.4/commons-lang-2.4.jar:/root/.m2/repository/org/codehaus/jackson/jackson-mapper-asl/1.9.4/jackson-mapper-asl-1.9.4.jar:/root/.m2/repository/org/apache/openjpa/openjpa-lib/2.1.1/openjpa-lib-2.1.1.jar:/root/.m2/repository/commons-pool/commons-pool/1.5.4/commons-pool-1.5.4.jar:/opt/cloudera/parcels/PHOENIX/lib/phoenix/phoenix-4.14.1-cdh5.16.2-thin-client.jar:/opt/cloudera/parcels/PHOENIX/lib/phoenix/phoenix-4.14.1-cdh5.16.2-client.jar:/etc/hadoop/conf:/etc/hive/conf:/etc/hbase/conf:/opt/cloudera/parcels/CDH/lib/hbase/lib/hbase-common-1.2.0-cdh5.16.2.jar:/etc/hbase/conf:/opt/cloudera/parcels/CDH/lib/hbase/lib/hbase-spark-1.2.0-cdh5.16.2.jar:/opt/cloudera/parcels/CDH/lib/hbase/lib/hbase-client-1.2.0-cdh5.16.2.jar:/opt/cloudera/parcels/CDH/lib/hbase/lib/hbase-protocol-1.2.0-cdh5.10.2.jar:/opt/cloudera/parcels/CDH/lib/hbase/lib/htrace-core-3.2.0-incubating.jar:/opt/cloudera/parcels/CDH/lib/hbase/lib/hbase-server-1.2.0-cdh5.16.2.jar site.ycsb.Client -db site.ycsb.db.JdbcDBClient -s -P workloads/workload{a-f} -P phoenix.properties`

# Workload A - 100k 

OVERALL, RunTime(ms), 122121  
OVERALL, Throughput(ops/sec), 818.8599831314843  
TOTAL_GCS_PS_Scavenge, Count, 19  
TOTAL_GC_TIME_PS_Scavenge, Time(ms), 245  
TOTAL_GC_TIME_%_PS_Scavenge, Time(%), 0.20062069586721368  
TOTAL_GCS_PS_MarkSweep, Count, 2  
TOTAL_GC_TIME_PS_MarkSweep, Time(ms), 68  
TOTAL_GC_TIME_%_PS_MarkSweep, Time(%), 0.055682478852940934  
TOTAL_GCs, Count, 21  
TOTAL_GC_TIME, Time(ms), 313  
TOTAL_GC_TIME_%, Time(%), 0.2563031747201546  
READ, Operations, 49835  
READ, AverageLatency(us), 2204.3722082873483  
READ, MinLatency(us), 1538  
READ, MaxLatency(us), 315135  
READ, 95thPercentileLatency(us), 3387  
READ, 99thPercentileLatency(us), 8783  
READ, Return=OK, 49835  
CLEANUP, Operations, 1  
CLEANUP, AverageLatency(us), 7014400.0  
CLEANUP, MinLatency(us), 7012352  
CLEANUP, MaxLatency(us), 7016447  
CLEANUP, 95thPercentileLatency(us), 7016447  
CLEANUP, 99thPercentileLatency(us), 7016447  
UPDATE, Operations, 50165  
UPDATE, AverageLatency(us), 23.555805840725604  
UPDATE, MinLatency(us), 4  
UPDATE, MaxLatency(us), 3309  
UPDATE, 95thPercentileLatency(us), 54  
UPDATE, 99thPercentileLatency(us), 122  
UPDATE, Return=OK, 50165  

# Workload B - 100k  

OVERALL, RunTime(ms), 204484  
OVERALL, Throughput(ops/sec), 489.03581698323586  
TOTAL_GCS_PS_Scavenge, Count, 13  
TOTAL_GC_TIME_PS_Scavenge, Time(ms), 103  
TOTAL_GC_TIME_%_PS_Scavenge, Time(%), 0.0503706891492733  
TOTAL_GCS_PS_MarkSweep, Count, 2  
TOTAL_GC_TIME_PS_MarkSweep, Time(ms), 73  
TOTAL_GC_TIME_%_PS_MarkSweep, Time(%), 0.035699614639776216  
TOTAL_GCs, Count, 15  
TOTAL_GC_TIME, Time(ms), 176  
TOTAL_GC_TIME_%, Time(%), 0.08607030378904951  
READ, Operations, 95079  
READ, AverageLatency(us), 2085.230734441885  
READ, MinLatency(us), 1524  
READ, MaxLatency(us), 248575  
READ, 95thPercentileLatency(us), 2693  
READ, 99thPercentileLatency(us), 5963  
READ, Return=OK, 95079  
CLEANUP, Operations, 1  
CLEANUP, AverageLatency(us), 1548800.0  
CLEANUP, MinLatency(us), 1548288  
CLEANUP, MaxLatency(us), 1549311  
CLEANUP, 95thPercentileLatency(us), 1549311  
CLEANUP, 99thPercentileLatency(us), 1549311  
UPDATE, Operations, 4921  
UPDATE, AverageLatency(us), 83.7984149563097  
UPDATE, MinLatency(us), 11  
UPDATE, MaxLatency(us), 1609  
UPDATE, 95thPercentileLatency(us), 184  
UPDATE, 99thPercentileLatency(us), 292  
UPDATE, Return=OK, 4921  

# Workload C - 100k  

OVERALL, RunTime(ms), 217517  
OVERALL, Throughput(ops/sec), 459.7341816961433  
TOTAL_GCS_PS_Scavenge, Count, 34  
TOTAL_GC_TIME_PS_Scavenge, Time(ms), 243  
TOTAL_GC_TIME_%_PS_Scavenge, Time(%), 0.11171540615216283  
TOTAL_GCS_PS_MarkSweep, Count, 2  
TOTAL_GC_TIME_PS_MarkSweep, Time(ms), 67  
TOTAL_GC_TIME_%_PS_MarkSweep, Time(%), 0.0308021901736416  
TOTAL_GCs, Count, 36  
TOTAL_GC_TIME, Time(ms), 310  
TOTAL_GC_TIME_%, Time(%), 0.1425175963258044  
READ, Operations, 100000  
READ, AverageLatency(us), 2133.92357  
READ, MinLatency(us), 1542  
READ, MaxLatency(us), 224895  
READ, 95thPercentileLatency(us), 2915  
READ, 99thPercentileLatency(us), 7083  
READ, Return=OK, 100000  
CLEANUP, Operations, 1  
CLEANUP, AverageLatency(us), 824.0    
CLEANUP, MinLatency(us), 824  
CLEANUP, MaxLatency(us), 824  
CLEANUP, 95thPercentileLatency(us), 824  
CLEANUP, 99thPercentileLatency(us), 824  

# Workload D - 100k  

OVERALL, RunTime(ms), 207920  
OVERALL, Throughput(ops/sec), 480.9542131589073  
TOTAL_GCS_PS_Scavenge, Count, 31  
TOTAL_GC_TIME_PS_Scavenge, Time(ms), 263  
TOTAL_GC_TIME_%_PS_Scavenge, Time(%), 0.1264909580607926  
TOTAL_GCS_PS_MarkSweep, Count, 2  
TOTAL_GC_TIME_PS_MarkSweep, Time(ms), 67  
TOTAL_GC_TIME_%_PS_MarkSweep, Time(%), 0.032223932281646786  
TOTAL_GCs, Count, 33  
TOTAL_GC_TIME, Time(ms), 330  
TOTAL_GC_TIME_%, Time(%), 0.15871489034243938  
READ, Operations, 94892  
READ, AverageLatency(us), 2114.16922395987  
READ, MinLatency(us), 1537  
READ, MaxLatency(us), 258047  
READ, 95thPercentileLatency(us), 2855  
READ, 99thPercentileLatency(us), 6859  
READ, Return=OK, 94892  
CLEANUP, Operations, 1  
CLEANUP, AverageLatency(us), 51280.0  
CLEANUP, MinLatency(us), 51264  
CLEANUP, MaxLatency(us), 51295  
CLEANUP, 95thPercentileLatency(us), 51295  
CLEANUP, 99thPercentileLatency(us), 51295  
INSERT, Operations, 5108  
INSERT, AverageLatency(us), 544.9731793265466  
INSERT, MinLatency(us), 18  
INSERT, MaxLatency(us), 818175  
INSERT, 95thPercentileLatency(us), 165  
INSERT, 99thPercentileLatency(us), 320  
INSERT, Return=OK, 5108  


# Workload E - 100k   

OVERALL, RunTime(ms), 6060051  
OVERALL, Throughput(ops/sec), 16.501511290911576  
TOTAL_GCS_PS_Scavenge, Count, 4026  
TOTAL_GC_TIME_PS_Scavenge, Time(ms), 35020  
TOTAL_GC_TIME_%_PS_Scavenge, Time(%), 0.5778829254077235  
TOTAL_GCS_PS_MarkSweep, Count, 3  
TOTAL_GC_TIME_PS_MarkSweep, Time(ms), 175  
TOTAL_GC_TIME_%_PS_MarkSweep, Time(%), 0.002887764475909526  
TOTAL_GCs, Count, 4029  
TOTAL_GC_TIME, Time(ms), 35195  
TOTAL_GC_TIME_%, Time(%), 0.580770689883633  
CLEANUP, Operations, 1  
CLEANUP, AverageLatency(us), 50928.0  
CLEANUP, MinLatency(us), 50912  
CLEANUP, MaxLatency(us), 50943  
CLEANUP, 95thPercentileLatency(us), 50943  
CLEANUP, 99thPercentileLatency(us), 50943  
INSERT, Operations, 5062  
INSERT, AverageLatency(us), 676.1266297905966  
INSERT, MinLatency(us), 15  
INSERT, MaxLatency(us), 804351  
INSERT, 95thPercentileLatency(us), 173  
INSERT, 99thPercentileLatency(us), 317  
INSERT, Return=OK, 5062  
SCAN, Operations, 94938  
SCAN, AverageLatency(us), 63744.165581748086  
SCAN, MinLatency(us), 7928  
SCAN, MaxLatency(us), 427519  
SCAN, 95thPercentileLatency(us), 162815  
SCAN, 99thPercentileLatency(us), 193663  
SCAN, Return=OK, 94938


# Workload F - 100k  

OVERALL, RunTime(ms), 217893  
OVERALL, Throughput(ops/sec), 458.9408562918497  
TOTAL_GCS_PS_Scavenge, Count, 35  
TOTAL_GC_TIME_PS_Scavenge, Time(ms), 414  
TOTAL_GC_TIME_%_PS_Scavenge, Time(%), 0.19000151450482575  
TOTAL_GCS_PS_MarkSweep, Count, 2  
TOTAL_GC_TIME_PS_MarkSweep, Time(ms), 63  
TOTAL_GC_TIME_%_PS_MarkSweep, Time(%), 0.02891327394638653  
TOTAL_GCs, Count, 37  
TOTAL_GC_TIME, Time(ms), 477  
TOTAL_GC_TIME_%, Time(%), 0.21891478845121232  
READ, Operations, 100000  
READ, AverageLatency(us), 2049.75395  
READ, MinLatency(us), 1553  
READ, MaxLatency(us), 243199  
READ, 95thPercentileLatency(us), 2561  
READ, 99thPercentileLatency(us), 5895  
READ, Return=OK, 100000  
READ-MODIFY-WRITE, Operations, 50078  
READ-MODIFY-WRITE, AverageLatency(us), 2078.6230081073527  
READ-MODIFY-WRITE, MinLatency(us), 1581  
READ-MODIFY-WRITE, MaxLatency(us), 129343  
READ-MODIFY-WRITE, 95thPercentileLatency(us), 2617  
READ-MODIFY-WRITE, 99thPercentileLatency(us), 5799  
CLEANUP, Operations, 1    
CLEANUP, AverageLatency(us), 6551552.0    
CLEANUP, MinLatency(us), 6549504    
CLEANUP, MaxLatency(us), 6553599    
CLEANUP, 95thPercentileLatency(us), 6553599  
CLEANUP, 99thPercentileLatency(us), 6553599  
UPDATE, Operations, 50078  
UPDATE, AverageLatency(us), 34.68852589959663  
UPDATE, MinLatency(us), 14  
UPDATE, MaxLatency(us), 2545  
UPDATE, 95thPercentileLatency(us), 71  
UPDATE, 99thPercentileLatency(us), 139  
UPDATE, Return=OK, 50078

