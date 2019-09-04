# arm-oraclelinux-wls-admin
 Simple deployment of a Weblogic Cluster Domain on multiple Oracle Linux VMs with Weblogic Server pre-installed

<table border="0">
<tr border="0">
    <td>
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fwls-eng%2Farm-oraclelinux-wls-cluster%2Fmaster%2Fclusterdeploy.json"" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
    </td>
    <td>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fwls-eng%2Farm-oraclelinux-wls-cluster%2Fmaster%2Fclusterdeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>
    </td>
  </tr>
</table>    

This template allows us to deploy Weblogic Cluster Domain on multiple Oracle Linux VMs with Weblogic Server (12.2.1.3.0) pre-installed. 
This template deploy by default, an A3 size VM in the resource group location and return the fully qualified domain name of the VM.

To install Weblogic Server, requires Oracle Weblogic Install kit and Oracle JDK to be downloaded, from OTN Site (https://www.oracle.com/technical-resources/). The OTN site requires the user to accept <a href="https://www.oracle.com/downloads/licenses/standard-license.html">OTN Free Developer License Agreement</a> before downloading any resources. 
So, when this template is run, user will be required to accept the <a href="https://www.oracle.com/downloads/licenses/standard-license.html">OTN Free Developer License Agreement</a> and also provide OTN credentials (username and password), to download the Oracle Weblogic Install Kit and Oracle JDK.


<h3>Using the template</h3>

**PowerShell** 

*#use this command when you need to create a new resource group for your deployment*

*New-AzResourceGroup -Name &lt;resource-group-name&gt; -Location &lt;resource-group-location&gt; 

*New-AzResourceGroupDeployment -ResourceGroupName &lt;resource-group-name&gt; -TemplateUri https://raw.githubusercontent.com/wls-eng/arm-oraclelinux-wls-cluster/master/clusterdeploy.json*

**Command line**

*#use this command when you need to create a new resource group for your deployment*

*az group create --name &lt;resource-group-name&gt; --location &lt;resource-group-location&gt;

*az group deployment create --resource-group &lt;resource-group-name&gt; --template-uri https://raw.githubusercontent.com/wls-eng/arm-oraclelinux-wls-cluster/master/clusterdeploy.json*

**Cluster domain configuration**
<p>Minimum 2 VMs  and maximum of 5 VMs involved for cluster domain setup.</p>
<p>Domain setup will be available at "/u01/domains/{domain name}" on each VMs
<p>1)Weblogic admin server will be hosted on as per user supplied for parameter adminVMName. By default name will be adminVM </p>
<p>2)Other VMs , depending on number of instances managed servers willbe hosted in VMs with name managed server prefix and index   </p>

**Accessing Admin Console**
<p>
Follow steps once after successful deployment.
 <p> You can refer the Outputs section of json file produced once after successful deployment
 <p> Access the weblogic console using </p>
 <p>   For non ssl access     : http://{public ip address or dns name}:7001/console </p>
 <p>   For secured/ssl access : https://{public ip address or dns name}:7002/console </p>
</p>

<h3> Adding another managed server to  running cluster domain </h3>

**PowerShell** 

*#use this command when you need to create a new resource group for your deployment*

*New-AzResourceGroupDeployment -ResourceGroupName &lt;resource-group-name&gt; -TemplateUri https://raw.githubusercontent.com/wls-eng/arm-oraclelinux-wls-cluster/master/addnodedeploy.json*

**Command line**

*#use this command when you need to create a new resource group for your deployment*

*az group deployment create --resource-group &lt;resource-group-name&gt; --template-uri https://raw.githubusercontent.com/wls-eng/arm-oraclelinux-wls-cluster/master/addnodedeploy.json*

<p>Note : </p>
 <p>1) Parameters dnsLabelPrefix, managedServerName and vmName should be unique. Better to follow the existing naming conventions as per existing cluster domain setup. </p>
 <p>2) adminURL should be supplied with {admin server public ip or dn name}:{ non ssl port} </p>
 

If you are new to Azure virtual machines, see:

- [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).
- [Azure Linux Virtual Machines documentation](https://docs.microsoft.com/azure/virtual-machines/linux/)
- [Azure Windows Virtual Machines documentation](https://docs.microsoft.com/azure/virtual-machines/windows/)
- [Template reference](https://docs.microsoft.com/azure/templates/microsoft.compute/allversions)
- [Quickstart templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Compute&pageNumber=1&sort=Popular)

If you are new to template deployment, see:

[Azure Resource Manager documentation](https://docs.microsoft.com/azure/azure-resource-manager/)
