# HDF-2.0-NiFi-Notification-Services

##Short Description:

Steps to configure NiFi Notification Services from Apache Ambari in HDF-2.x version

##Introduction

When the NiFi bootstrap starts or stops NiFi, or detects that it has died unexpectedly, it is able to notify configured recipients. Currently, the only mechanism supplied is to send an e-mail notification.

##Prerequisite

1) Assuming you already have HDF-2.x Installed on your VM/Server, Ambari, NiFi is up and running with out security.

If not, I would recommend "Ease of Deployment" section of [this](https://community.hortonworks.com/articles/57980/hdf-20-apache-nifi-integration-with-apache-ambarir.html) article to install it [You can also follow this [article](https://community.hortonworks.com/articles/56849/automate-deployment-of-hdf-20-clusters-using-ambar.html) for Automated installation of HDF cluster or refer hortonworks.com for detailed steps]

##Configuring NiFi property files in Ambari

1) To setup email notifications we have to update only two configurations file bootstrap.conf and bootstrap-notification-services.xml

2) We have to update appropriate properties in Ambari to configure it, first we have to edit Template for bootstrap.conf to update below properties. Uncomment below lines in the properties file:

```
nifi.start.notification.services=email-notification 
nifi.stop.notification.services=email-notification
nifi.dead.notification.services=email-notification
```

3) Edit Template for bootstrap-notification-services.xml and make sure your SMTP settings are updated, and are uncommented. Sample configuration is given below:

```
<service> 
<id>email-notification</id> 
<class>org.apache.nifi.bootstrap.notification.email.EmailNotificationService</class> 
<property name="SMTP Hostname">west.xxxx.server.net</property> 
<property name="SMTP Port">587</property> 
<property name="SMTP Username">jgeorge@hortonworks.com</property> 
<property name="SMTP Password">Th1sisn0tmypassw0rd</property>   
<property name="SMTP TLS">true</property> 
<property name="From">jgeorge@hortonworks</property> 
<property name="To">jgeorge@hortonworks.com</property> 
</service>
```