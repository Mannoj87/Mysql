# Mysql Failover Module (Minor Change)
---------------------------------------

- Check for Mysql Failover rpm and grep for topology.py 
- Tested and works fine in RHEL7 using Mysql 5.6 with GTID enabled using mysql-utilities-1.6.5-1.el7

Check: 
[root@master ~]# rpm -qlp /tmp/mysql-utilities-1.6.5-1.el7.noarch.rpm  | grep -i topology.py
                

Result: 
/usr/lib/python2.7/site-packages/mysql/utilities/common/topology.py


### To further test if ReadOnly is changed to ReadWrite

   - Copy the file contents as per in https://github.com/Mannoj87/Mysql/blob/master/Mysql_Failover/topology.py to local topology.py
   - Keep Master in RW mode and all slaves in RO mode using (set global read_only=1 or 0 ) 
   - Start mysqlfailover daemon 
   - Purposely bring down Master
   - After automatic failover
   - Check Newly elected Master read_only variable using (show variables like '%read_only%';) it should be OFF

### Modified Changes Rebuilt the RPM and Uploaded in above rpm 
https://github.com/Mannoj87/Mysql/blob/master/Mysql_Failover/mysql-utilities-1.6.5-1.el7.noarch.rpm

This rpm Requires: mysql-connector-python >= 2.0.0 as a dependency package. You may download from https://dev.mysql.com/downloads/connector/python/
