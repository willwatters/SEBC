Start the Cloudera Manager server. Then in challenges/labs/2_db.properties.md:
Add the first line from your server log



```
[root@ip-172-31-47-28 cloudera-scm-server]# systemctl start cloudera-scm-server

[root@ip-172-31-47-28 cloudera-scm-server]# head /var/log/cloudera-scm-server/cloudera-scm-server.log
2018-10-19 09:04:43,383 INFO main:com.cloudera.server.cmf.Main: ================================================================================
2018-10-19 09:04:43,393 INFO main:com.cloudera.server.cmf.Main: Starting SCM Server. JVM Args: [-Dlog4j.configuration=file:/etc/cloudera-scm-server/log4j.properties, -Dfile.encoding=UTF-8, -Dcmf.root.logger=INFO,LOGFILE, -Dcmf.log.dir=/var/log/cloudera-scm-server, -Dcmf.log.file=cloudera-scm-server.log, -Dcmf.jetty.threshhold=WARN, -Dcmf.schema.dir=/usr/share/cmf/schema, -Djava.awt.headless=true, -Djava.net.preferIPv4Stack=true, -Dpython.home=/usr/share/cmf/python, -XX:+UseConcMarkSweepGC, -XX:+UseParNewGC, -XX:+HeapDumpOnOutOfMemoryError, -Xmx2G, -XX:MaxPermSize=256m, -XX:+HeapDumpOnOutOfMemoryError, -XX:HeapDumpPath=/tmp, -XX:OnOutOfMemoryError=kill -9 %p], Args: [], Version: 5.14.4 (#3 built by jenkins on 20180707-0445 git: 0971e84bdceb60db9b96533f46451f40ed8cbdf9)
2018-10-19 09:04:43,462 INFO main:org.mortbay.log: Logging to org.slf4j.impl.Log4jLoggerAdapter(org.mortbay.log) via org.mortbay.log.Slf4jLog
2018-10-19 09:04:43,578 INFO main:org.springframework.context.support.ClassPathXmlApplicationContext: Refreshing org.springframework.context.support.ClassPathXmlApplicationContext@2f375701: startup date [Fri Oct 19 09:04:43 UTC 2018]; root of context hierarchy
2018-10-19 09:04:43,626 INFO main:org.springframework.beans.factory.xml.XmlBeanDefinitionReader: Loading XML bean definitions from class path resource [webapp/WEB-INF/spring/beanRefFactory.xml]
2018-10-19 09:04:43,980 INFO main:org.springframework.beans.factory.support.DefaultListableBeanFactory: Pre-instantiating singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@52c71145: defining beans [bootstrapContext,rootContext]; root of factory hierarchy
2018-10-19 09:04:44,003 INFO main:org.springframework.context.support.GenericApplicationContext: Refreshing org.springframework.context.support.GenericApplicationContext@21bab96e: startup date [Fri Oct 19 09:04:44 UTC 2018]; root of context hierarchy
2018-10-19 09:04:44,004 INFO main:org.springframework.beans.factory.support.DefaultListableBeanFactory: Pre-instantiating singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@62afaca6: defining beans [commandLineConfigurationBean,entityManagerFactoryBean,com.cloudera.server.cmf.TrialState,com.cloudera.server.cmf.TrialManager,com.cloudera.cmf.crypto.LicenseLoader]; root of factory hierarchy
2018-10-19 09:04:44,070 INFO main:com.cloudera.enterprise.CommonMain: Reading database properties from /etc/cloudera-scm-server/db.properties
2018-10-19 09:04:44,073 INFO main:com.cloudera.enterprise.CommonMain: Statistics not enabled, c3p0 JMX disabled
```

Add the log line that contains the phrase "Started Jetty server"

```
[root@ip-172-31-47-28 cloudera-scm-server]# cat /var/log/cloudera-scm-server/cloudera-scm-server.log | grep -i 'Started Jetty server'
2018-10-19 09:05:38,768 INFO WebServerImpl:com.cloudera.server.cmf.WebServerImpl: Started Jetty server.
```


Push to your GitHub repo and label the Issue 'submitted`
Assign the issue to the instructors
