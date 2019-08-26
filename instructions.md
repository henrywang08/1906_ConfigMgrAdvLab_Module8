#WorkshopPLUS - System Center Configuration Manager: Concepts and Administration Advanced (1902)

#Module 8, Lab 1, Exercise 1 - Global Data Replication

##Scenario
The IT Administrator of Contoso.com is keen to see the changes in site-to-site replication, and so decides to create a new collection to start replication.

> In this exercise you will:  
- Demonstrate how global data, such as collection defination, is replicated.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++



1. []Click Configuration Manager Console icon from Taskbar.



1. []In **Configuration Manager Console**, click **Assets and Compliance** workspace. Right-click **Device Collections** and select **Create Device Collection**.


1. []On the **General** page of **Create Device Collection Wizard**, configure as below, then click **Summary**. Click OK for "**Configuration Manager**" warning message.  
	- **Name:** *Collection in NYC Site*  
	- **Limiting Collection:** *All Desktop and Server Clients*

1. []On **Summary** page, review the settings, click **Next**
1. []On **Completion** page, click **Close**



	>Switch to @lab.VirtualMachine(NYCPR2).SelectLink

1. []Log on to **NYCPR2** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []Click Configuration Manager Console icon from Taskbar.


1. []In **Configuration Manager Console**, click **Assets and Compliance** workspace, click **Device Collections** node.

	> [!ALERT] Note: You may need wait for about five minutes, and refresh Device Collections view on NYCPR2 to see the new collection.

	> [!KNOWLEDGE] **Question**: Will you see collection "Collection in NYC Site" in PR2 site? Why?  
	>    
	>  **Answer**: Collection definition is one part of Global Data, which will be replicated to all sites in the hierarchy.

	!IMAGE[Screenshot](screens/920719.jpg)



**Congratulations!  **
   
 You have successfully:  
   

- Demonstrated how global data, such as collection defination, is replicated.

Click **Next** to advance to the next exercise.

===

#Module 8, Lab 1, Exercise 2 - View Database Replication Status

##Scenario
The IT Administrator in Contoso.com is interested in looking at how IT departments can use the Configuration Manager console to view the database replication status between sites.

>
In this exercise you will:  
- Verify that the Configuration Manager databases have replicated successfully

> Switch to @lab.VirtualMachine(NYCCAS).SelectLink

1. []Log on to **NYCCAS** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++



1. []Click Configuration Manager Console icon from Taskbar.


1. []In Configuration Manager Console, click **Monitoring** workspace and select **Database Replication** node.


1. []On **Results** pane of **Database Replication** node, select the row where **Child Site** column is **PR2**. Click **Replication Link Analyzer** from Ribbon.

	!IMAGE[Screenshot](screens/920723.jpg)


1. []Review **Replication Link Analyzer** report.

	!IMAGE[Screenshot](Screens/rpuzldfl.jpg)

**Note: Ignore message "Check if change tracking records are cleaned up on sql server".**	


> Switch to @lab.VirtualMachine(NYCPR2).SelectLink

1. []Log on to **NYCPR2** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++



1. []In **Server Manager**, click **Tools** menu, select **Services**.
1. []Right click **SMS\_EXECUTIVE** service, select **Stop**.

	!IMAGE[Screenshot](screens/4122b75b.jpg)

	> Switch to @lab.VirtualMachine(NYCCAS).SelectLink

1. []Log on to **NYCCAS** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []In Configuration Manager Console, click **Monitoring** workspace and select **Database Replication** node. Refresh the node after about 5 minutes. The **Link State** between CAS &lt;-&gt; PR2 will change to **Link Degraded**.



1. []On Results pane of **Database Replication** node, select the row where **Child Site** column is **PR2**. Click **Replication Link Analyzer** from Ribbon.

	!IMAGE[Screenshot](screens/920729.jpg)


1. []View the Replication Link Analyzer result.

	!IMAGE[Screenshot](screens/9f6d403e.jpg)


	
1. []Click **Restart the SMS\_EXECUTIVE service** in **CAS &lt;-&gt; PR2 Replication Link Analyzer** window.
1. []Click **Continue.**
1. []Click **OK** in **Replicaiton Link Analyzer** window.
1. []Click **Check to see if the problem** **is fixed** in **CAS &lt;-&gt; PR2 Replication Link Analyzer** window.

1. []click **Close** to close Replication Link Analyzer window.

	!IMAGE[Screenshot](Screens/tovna5s3.jpg)

**Note: Ignore message "Check if change tracking records are cleaned up on sql server".**	


1. []Select database replication link CAS &lt;-&gt; PR2. Click **Refresh** in Ribbon. The **Link State** will change back to **Link Active** in about 5 minutes.

	> [!KNOWLEDGE] Here are some addtional information about Link State:  
	>    
	>  Link Active - No issues have been detected and communication across the site link is currently active.  
	>    
	>  Link Degraded - Replication between the sites is functional, but at least one object that needs to be replicated has been delayed. Monitor the links in this state and review information from both sites involved for indications that the link might fail.  
	>    
	>  Link Failed - Replication between the sites is not functional.

	!IMAGE[Screenshot](Screens/50eizqs4.jpg)


1. []Right click empty space on Taskbar, select **Show the desktop**. 

1. []Open **ReplicationLinkAnalysis.log** file to view the content.

1. []Double click **ReplicationAnalysis.htm** file to view the content.

	!IMAGE[Screenshot](Screens/zh0hrfvm.jpg)


**Congratulations!  **
   
 You have successfully:  
   

- View Database Replication Status

Click **Next** to advance to the next exercise.

===

#Module 8, Lab 1, Exercise 3 - Reinitialize DRS Replication

##Scenario
Following an outage, the IT Administrator in Contoso.com wants to reinitialize the DRS Replication service for Configuration Manager sites to replicate properly.

>
In this exercise you will:  
- Successfully reinitialize the DRS Replication service.

> Switch to @lab.VirtualMachine(NYCPR2).SelectLink

1. []Log on to **NYCPR2** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []Click **SQL Server Management Studio 17** icon on taskbar to launch it.


1. []In **Microsoft SQL Sever Management Studio**, connect to **NYCPR2** as **Database Engine.**
1. []Click **File**, click **New**, and then click **Query with Current Connection**.
1. []Type the SQL command in the query window - +++*EXEC CM\_PR2.dbo.spDrsSendSubscriptionInvalid 'PR2', 'CAS', 'Configuration Data'*+++
1. []Click **Query** and then click **Execute**. The result will show 0. Record the timestamp when you see the result.

	!IMAGE[Screenshot](Screens/ygr4xb3c.jpg)


	> Switch to @lab.VirtualMachine(NYCCAS).SelectLink

1. []Log on to **NYCCAS** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []Click CMTrace.exe icon from Taskbar.

	!IMAGE[Screenshot](screens/a5c371f4.jpg)

1. []In **Configuration Manager Trace Log Tool** window, click **File** and then click **Open**.

1. []Browse and open *\\\\NYCCAS\\SMS\_CAS\\Logs\\rcmctrl.log* file.


1. []Click **Tools** and then click **Find**.

1. []Search up for "+++*Checking if we need to create an initialization+++"*. You will find a message "**Checking if we need to create an initialization package for replication group Configuration Data for site PR2**" logged within 5 minutes after you execute the SQL command on NYCPR2.
	
	!IMAGE[Screenshot](Screens/bj3vwyev.jpg)


1. []View the messages below "**Checking if we need to create an initialization package for replication group Configuration Data for site PR2**". You will see BCP is used to export the global configuration data tables to files. 

	> [!KNOWLEDGE] BCP -  The bulk copy program utility \(bcp\) bulk copies data between an instance of MicrosoftSQL Server and a data file in a user-specified format.  
	>    
	>  bcp Utility  
	>  https://msdn.microsoft.com/en-us/library/ms162802.aspx

	!IMAGE[Screenshot](Screens/nstrtgp0.jpg)



1. []In **Configuration Manager Trace Log Tool** window, click **File** and then click **Open**.
1. []Browse and open *\\\\NYCCAS\\SMS\_CAS\\Logs\\schedule.log* file.
	
1. []Click **Tools** and then click **Find**

1. []Search up for "+++*DRS Initialization for Site \[PR2\]*+++". You may see several "**DRS Initialization for Site \[PR2\]**" messages in the log files, while the first related message should be within 5 - 10 minutes after you execute the SQL command on NYCPR2.

	!IMAGE[Screenshot](Screens/xnhpys2f.jpg)

1. []In **Configuration Manager Trace Log Tool** window, click **File** and then click **Open**.

1. []Browse and open *\\\\NYCCAS\\SMS\_CAS\\Logs\\sender.log* file.
	
1. []Click Tools and then click Find
1. []Search up for "+++*CabFiles\\PR2\_*+++". You may see one message like "**Package file = E:\\Program Files\\Microsoft Configuration Manager\\inboxes\\rcm.box\\CabFiles\\PR2\_.cab**".
	
	!IMAGE[Screenshot](Screens/s2hx5qax.jpg)

1. []View the messages below &quot;**Package file = E:\\Program Files\\Microsoft Configuration Manager\\inboxes\\rcm.box\\CabFiles\\PR2\_<guid>.cab</guid>**&quot;.

	> [!KNOWLEDGE] Note: You will find message like &quot;**Wrote 230212 bytes to \\\\NYCPR2.CONTOSO.COM\\SMS\_SITE\\1002VCAS.PCK at position 2829312**&quot;, before message &quot;**Sending completed \[E:\\Program Files\\Microsoft Configuration Manager\\inboxes\\rcm.box\\CabFiles\\PR2\_<guid>.cab</guid>**&quot;. 

	!IMAGE[Screenshot](Screens/f1nu0ahz.jpg)

	> Switch to @lab.VirtualMachine(NYCPR2).SelectLink

1. []Log on to **NYCPR2** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []If SQL Management Studio is closed, open **SQL Server Management Studio** 17 on taskbar to launch it.

1. []In **Microsoft SQL Sever Management Studio**, connect to **NYCPR2** as **Database Engine**.
1. []Click **File**, click **New**, and then click **Query with Current Connection**.
1. []Type the following SQL command in the query window - +++*Select top 1000 LogTime, LogText from CM\_PR2.dbo.vLogs where LogText like '%Invalid%' order by LogTime desc*+++
1. []Click **Query** menu and then click **Execute**. The result will show you the trigger of the global configuration data reinitilization.
	
	

	!IMAGE[Screenshot](Screens/45ckznfi.jpg)


1. []In **Microsoft SQL Sever Management Studio**, click **File**, click **New**, and then click **Query with Current Connection**.

1. []Type the following SQL command in the query window - +++*Select top 1000 LogTime, LogText from CM\_PR2.dbo.vLogs where LogText like '%BCP%' order by LogTime desc*+++

1. []Click **Query** menu and then click **Execute**. The result will show when the re-initialized global configuration data package is applied.
	

	
	!IMAGE[Screenshot](Screens/b4qpaa52.jpg)


	> Switch to @lab.VirtualMachine(NYCCAS).SelectLink

1. []Log on to **NYCCAS** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []Click Configuration Manager Console icon from Taskbar.



1. []In Configuration Manager Console, click **Monitoring** workspace and select **Database Replication** node. Verify the replication **Link State** between CAS &lt;-&gt; PR2 is **Link Active**.


	!IMAGE[Screenshot](Screens/mzy0p3yn.jpg)


1. []In Configuration Manager Console, click **Monitoring** workspace and select **Site Hierarchy** node. Verify all sites are green.

	!IMAGE[Screenshot](Screens/kdtm2hkc.jpg)



**Congratulations!  **
   
 You have successfully:  
   

- Reinitialize DRS Replication

Click **Next** to advance to the next exercise.

===

#Module 8, Lab 2, Exercise 1 - Configure Certificates for Site System Roles with IIS Installed

##Scenario
The IT Administrator in Contoso.com is asked to configure the certificates on Site Server Roles that requires IIS.

>
In this exercise you will:  
- Configure the required certificates on Site System roles requiring IIS

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []In **Server Manager** console, click **Tools** menu, select **Internet Information Services \(IIS\) Manager** to launch it.

1. []Expand **NYCCFG \(CONTOSO\\administrator\).**

1. []Expand **Sites**, right-click **Default Web Site** and then select **Edit Bindings**.

1. []Click **https** type and select **Edit**

1. []On the **Edit Site Binding** dialog box, under **SSL certificate,** click **Not selected** to expand the dropdown menu, and select the certificate "3B86E76921A1B6EA94DC028FD41359B692C8A597". Click OK.

	> [!KNOWLEDGE] Note: The select ceritificte 3B86E76921A1B6EA94DC028FD41359B692C8A597 is created using **ConfigMgr Web Server** certificate template. You can click **View** in **Edit Site Biding** dialog box, on the **Certificate** window, click **Details** tab, select **Extensions Only** in **Show:** drop-down list, click **Certificate Template Information** in the **Field** column. You should see the template name is **ConfigMgr Web Server**.

	!IMAGE[Screenshot](screens/920759.jpg)


	> Switch to @lab.VirtualMachine(NYCCAS).SelectLink

1. []Log on to **NYCCAS** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++


1. []In **Server Manager** console, click **Tools** menu, select **Internet Information Services \(IIS\) Manager** to launch it.


1. []Expand **NYCCAS \(CONTOSO\\administrator\).**

1. []Expand **Sites**, right-click **WSUS Administration** and then select **Edit Bindings**.

1. []Click **https** type and select **Edit**

1. []On the **Edit Site Binding** dialog box, under **SSL certificate,** click **Not selected** to expand the dropdown menu, and select the certificate start with "**C716**". Click **OK**.
	
	
	

	> [!KNOWLEDGE] Note: The select ceritificte start with **C716** is created using **ConfigMgr Web Server** certificate template. You can click **View** in **Edit Site Binding**. diaglog box, on the **Certificate** window, click **Details** tab, select **Extensions Only** in **Show:** drop-down list, click **Certificate Template Information** in the **Field** column. You should see the template name is **ConfigMgr Web Server**.

	!IMAGE[Screenshot](screens/c96177fe.jpg)



	> Switch to @lab.VirtualMachine(NYCDC).SelectLink

1. []Log on to **NYCDC** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []In **Server Manager** console, click **Tools** menu, select **Internet Information Services \(IIS\) Manager** to launch it.


1. []Expand **NYCDC \(CONTOSO\\administrator\).** 

1. []Expand **Sites**, right-click **Default Web Site**, select **Edit Bindings**.
1. []Click **Add..** button.
1. []In **Add Site Binding** dialog box, under **Type**, select **https**. Under **SSL certificate,** click **Not selected** to expand the dropdown menu, and select the certificate start with "**5444**". Click **OK**. Click **Close**.
	
	
	

	> [!KNOWLEDGE] Note: The select ceritificte is created using **ConfigMgr Web Server** certificate template. You can click **View** in **Edit Site Biding** dialog box, on the **Certificate** window, click **Details** tab, select **Extensions Only** in **Show:** drop-down list, click **Certificate Template Information** in the **Field** column. You should see the template name is **ConfigMgr Web Server**.

	!IMAGE[Screenshot](screens/f1fae9f4.jpg)



**Congratulations!  **
   
 You have successfully:  
   

- Configure Certificates for Site System with IIS Installed

Click **Next** to advance to the next exercise.

===

#Module 8, Lab 2, Exercise 2 - Enable HTTPS for Client Communication

##Scenario
After satisfying all the required certificate prerequisites, the IT Administrator of Contoso.com decides to enable HTTPS client communication for the Configuration Manager site.

>
In this exercise you will:  
- Configure the Configuration Manager site to use HTTPS for client communication.
 

 
 
>Switch to @lab.VirtualMachine(NYCCAS).SelectLink


1. []Log on to **NYCCAS** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++


1. []Click Configuration Manager Console icon from Taskbar.

	!IMAGE[Screenshot](screens/5eeb97c0.jpg)


1. []Click **Administration** workspace, expand **Site Configuration**.
1. []Click **Sites**, select "**NYC - Contoso NYC Primary Site**" in result pane. Click **Properties** in the ribbon.
1. []Click **Client Computer Communication** tab, select **HTTPS only**. Click **OK**.

	!IMAGE[Screenshot](screens/a4e8cd66.jpg)

1. []Click **Servers and Site System Roles**, select **\\\\NYCCFG.CONTOSO.COM**
1. []Under **Site System Roles**, select **Distribution point**. Click **Properties** in the ribbon.
1. []Select **Import certificate**. Type the following information, then click **OK**.
	
	  - **Certificate**: *\\\\nyccfg\\e$\\nyccfg\_dpcert.pfx*
	  - **Password**: +++*Pa$$w0rd*+++
	
1. []Click **Yes** if there is a warning "**The certificate you specified is already in use**".
	
	
	

	!IMAGE[Screenshot](screens/35585bc9.jpg)


	> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++


1. []Open **Server Manager**, click **Tools** menu, click **Services**.  
1. []Right click **SMS Agent Host** service, select **Restart**.


	> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Log on to **NYCCL1** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++



1. []Right click Start icon, select **Computer Management**.  
1. []Expand **Services and Applications**, click **Services**.  
1. []Right click **SMS Agent Host** service, select **Restart**.


	> Switch to @lab.VirtualMachine(NYCDC).SelectLink

1. []Log on to **NYCDC** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []Open **Server Manager**, click **Tools** menu, click **Services**.  
1. []Right click **SMS Agent Host** service, select **Restart**.
 

	> Switch to @lab.VirtualMachine(NYCCAS).SelectLink

1. []Log on to **NYCCAS** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++



1. []Open **Server Manager**, click **Tools** menu, click **Services**.  
1. []Right click **SMS Agent Host** service, select **Restart**.

 
	> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Log on to **NYCCL1** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: +++Pa$$w0rd+++

1. []Right click Start icon, click search, type *Control Panel,* then select **Control Panel**
1. []Click **System and Security**, then click **Configuration Manager**.
1. []Verify **Client certificate** property value is **PKI**.

	!IMAGE[Screenshot](screens/eb2323d4.jpg)

 
	> Switch to @lab.VirtualMachine(NYCCAS).SelectLink

1. []Log on to **NYCCAS** using the following credentials:  
	- **User name**: Contoso\\Administrator  
	- **Password**: Pa$$w0rd

1. []In Configuration Manager console, click **Assets and Compliance** workspace. Click **Devices**.
1. []Right click menu bar on **Client Activity**, select **Last Online Time**.
1. []You should see all clients Icon are showing green, and the Last Online Time will be within 10 minutes after you restart SMS Agent service on NYCCFG. If not all clients icon are showing green, wait for another 10 minutes before refresh. You may also check **CcmNotificationAgent.log** on the SCCM client to verify if there is a "**Successfully sent keep-alive message**" message.
	
	
	

	!IMAGE[Screenshot](screens/d0f0b4ed.jpg)



**Congratulations!  **
   
 You have successfully:  
   

- Enable HTTPS for Client Communication

Click *Continue* to advance to the next exercise.