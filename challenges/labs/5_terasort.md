Challenge 5 - Kerberize the cluster

Create the Issue Kerberize cluster
Assign the issue to yourself and label it started
You must use AES256
Install an MIT KDC on the same node as the MySQL server
Name your realm after your GitHub handle
Use SG as a suffix
For example: MFERNEST.SG
Create Kerberos principals for raffles, fullerton, and cloudera-scm
Give cloudera-scm the privileges needed to create principals and keytabs
Enable Kerberos for the cluster
Run the terasort program as raffles using /user/raffles/tgen512m
Copy the command and output to challenges/labs/5_terasort.md
Run the Hadoop pi program as the user fullerton
Copy the command and output to challenges/labs/5_pi.md
Copy only text files in /var/kerberos/krb5kdc/ to your repo as follows:
Add the prefix 5_ and the suffix .md
Example: 5_kdc.conf.md
Push this work to your GitHub repo and label the Issue submitted
Assign the issue to the instructors
