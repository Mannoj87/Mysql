### How to unpack the RPM from Mysql and Edit it and Pack it back.

yum install rpm-build rpmdevtools
rpmdev-setuptree
tree rpmbuild

vi ~/.rpmmacros
%packager MANNOJ
%_topdir /root/rpmbuild
%_tmppath /root/rpmbuild/tmp



rpmrebuild -e -p mysql-utilities-1.6.5-1.el7.noarch.rpm  #FROM MYSQL

mkdir -p /tmp/NEWMAKERPM/
cp mysql-utilities-1.6.5-1.el7.noarch.rpm /tmp/NEWMAKERPM/

rpm2cpio mysql-utilities-1.6.5-1.el7.noarch.rpm | cpio -i --make-directories

make changes to /tmp/NEWMAKERPM/usr/lib/python2.7/site-packages/mysql/utilities/common/topology.py 
Save changes

cp -r /tmp/NEWMAKERPM/usr ~/rpmbuild/SOURCES/
cd ~/rpmbuild/


vi ~/rpmbuild/SPECS/mannoj_failover.spec


In another terminal - 

rpmrebuild -e -p mysql-utilities-1.6.5-1.el7.noarch.rpm  #FROM MYSQL

You will find a temp file in ~/.tmp/rpmrebuild.66257/work/spec.2 .

In another terminal - 
cat the file ~/.tmp/rpmrebuild.66257/work/spec.2 


Get back to first terminal 
$vi ~/rpmbuild/SPECS/mannoj_failover.spec
Copy the contents from  ~/.tmp/rpmrebuild.66257/work/spec.2  to ~/rpmbuild/SPECS/mannoj_failover.spec
     Save it.
:wq!


cp -r SOURCES/usr BUILDROOT/
mkdir -p BUILDROOT/mysql-utilities-1.6.5-1.el7.x86_64
rpmbuild -ba SPECS/mannoj_failover.spec

ls -ltr /root/rpmbuild/RPMS/noarch/mysql-utilities-1.6.5-1.el7.noarch.rpm



