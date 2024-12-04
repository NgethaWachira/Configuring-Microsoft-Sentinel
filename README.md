## Objective
To offer guidance through the process of setting up and configuring Microsoft Sentinel in Azure for security monitoring and data collection.
I show practical steps for configuring Sentinel to monitor, analyze, and store security-related data in an Azure environment.

### Skills Learned
- Set up the necessary components, including Log Analytics Workspace and Microsoft Sentinel Workspace.
  
- Manage roles and permissions using Azure's Identity and Access Management (IAM).
  
- Configure various data connectors for collecting log and security data from different resources, including third-party connectors.

- Install connectors for different systems (e.g., Microsoft Defender for Cloud, Windows security events, threat intelligence).

- Set up custom log ingestion and rules for collecting data from custom sources using Azure's data collection endpoints.

### Tools Used
<div>
<img src="https://img.shields.io/badge/-Microsoft%20Sentinel-0078D4?&style=for-the-badge&logo=Microsoft%20Azure%20DevOps&logoColor=white" alt="Microsoft Sentinel">
<img src="https://img.shields.io/badge/-Azure%20Portal-e6e600?&style=for-the-badge&logo=Microsoft%20Azure&logoColor=white" alt="Azure Portal">
<img src="https://img.shields.io/badge/-Log%20Analytics%20Workspace-ff6600?&style=for-the-badge&logo=Microsoft%20Azure&logoColor=white" alt="Log Analytics Workspace">
<img src="https://img.shields.io/badge/-Access%20Control%20(IAM)-00ff55?&style=for-the-badge&logo=Microsoft%20Azure&logoColor=white" alt="Access Control (IAM)">
<img src="https://img.shields.io/badge/-Microsoft%20Defender%20for%20Cloud-77773c?&style=for-the-badge&logo=Microsoft%20Defender&logoColor=white" alt="Microsoft Defender for Cloud">
<img src="https://img.shields.io/badge/-Pulsedive-666699?&style=for-the-badge&logo=pulsedive&logoColor=white" alt="Pulsedive">
</div>

## Steps
- We first ensure that we have a Microsoft account, an Azure subscription to use Microsoft sentinel, which has a valid payment method linked. This can 
be used for billing when using Azure resources like Sentinel and Log Analytics. Next we create a Log Analytics workspace to store the logs and data 
that Microsoft Sentinel will use for security monitoring, investigation, and analysis. In Azure portal click on Create a resource, In the search bar, 
type Log Analytics workspace and select it, Click Create and start the configuration.

<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/4944d7ec12ed6f4fdb1790dfab9cf06a22aee842/Images/Creating%20Log%20Workspace.PNG" width="700" />
</p>

- In the resource view you can see the workspace created according to how we've named it. Once we create our Log Analytics workspace, we go to Microsoft
  Sentinel in the Azure portal and add Microsoft Sentinel. Select the Log Analytics workspace you just created and follow the prompts to enable
  Sentinel. We are now ready to configure Microsoft Sentinel to start collecting and analyzing our security data.
  
<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/672389291bb433d2c2e05c53ef0cba9e0ae77ffd/Images/Adding%20sentinel%20to%20a%20workspace.PNG" width="300" />
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/672389291bb433d2c2e05c53ef0cba9e0ae77ffd/Images/Workplace%20setup.PNG" width="300" />
</p>

- Next we configure Role Management in Sentinel to assign roles to users through Azure's Access Control (IAM). This ensures that users have the correct
  permissions to manage or monitor Microsoft Sentinel based on their roles. On Azure portal got to Resource groups and select the SentinelRG resource
  group we created. Find and click the Access control (IAM). Under the Access control (IAM), we see the Role assignments that lists all the users and
  groups that currently have roles assigned within the resource group.

<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/279db7dc474299dab4034f2eb3958287634c69d6/Images/Access%20control%20role%20asignments.PNG" width="700" />
</p>

- Next we add roles to users and groups that don't have the required roles. Click Add at the top of the Role assignments pane a dn configure as you see fit.
  Choose the appropriate role for the user. For Microsoft Sentinel, roles like Microsoft Sentinel Contributor or Security Reader might be appropriate.
  To filter by Microsoft roles, you can type “Microsoft Sentinel” in the Role search box.

<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/506dfdef174a27277967a43c1d4ab195a83aed10/Images/Adding%20role%20assignment.PNG" width="300" />
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/506dfdef174a27277967a43c1d4ab195a83aed10/Images/Assigning%20roles%20to%20a%20user.PNG" width="300" />
</p>

- After the role is assigned, verify that the new role appears in the Role assignments section under the Access control (IAM) blade. We now have
  the permissions associated with the role, we are able to manage Microsoft Sentinel since we are assigned as a Microsoft Sentinel Contributor.

<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/4b04491e5cdf7bd3313a2fcdb1b2e2270ae323fd/Images/Role%20assigned%20to%20Azure%20ATP...as%20a%20contributor.PNG" width="700" />
</p>

- Since Sentinel uses the Log analytics workspace to store information, we then configure Log analytics workspace particularly for managing the log data
stored in the tables. We navigate and click Log Analytics Workspace in Azure portal, under the settings section look for Tables and click on it. This will
show you a list of all the tables within your Log Analytics workspace. The tables store various types of log data, such as security logs, audit logs, and
other telemetry data.

<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/86b0dd2d521e8a39211a495e07c4860901bacc40/Images/Storing%20log%20data%20under%20tables.PNG" width="700" />
</p>

- To nanage Log Data Stored in Tables, Click on any table to view its schema, we can use Kusto Query Language (KQL) to query and analyze the data stored
in these tables. We then set the retention period for each table's data to configure how long data should be kept in the workspace before being automatically deleted.
NOte: After configuring the tables and data, we can set up alerts, create workbooks, and dashboards in Microsoft Sentinel based on the log data from these tables.

<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/ca97ee208166c4e91e73c555825bb60af5a32cda/Images/Security%20event%20table.PNG" width="300" />
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/ca97ee208166c4e91e73c555825bb60af5a32cda/Images/Log%20retention%20settings.PNG" width="300" />
</p>

- Next we install data connectors, we'll use the Microsoft Sentinel Training Lab Solution. It' a pre-packaged solution that provides sample data and
configurations for training purposes. We find it in Azure portal, type Microsoft Sentinel in the search bar and open our Workspace, Go to Content Management,
 and open Content Hub, type training in the search bar to find the Microsoft Sentinel Training Lab Solution.

<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/38ba5e709a278be62c37b42c81f877268b1ca4e4/Images/Data%20connectors.PNG" width="700" />
</p>

- We then select and install the Microsoft Sentinel Training Lab Solution, selecting the appropriate Resource Group and Sentinel Workspace during the setup,
review the settings, and once you're satisfied, click Create. After the Lab solution is installed, go back to your Content Hub in Content Management.
You should see the Microsoft Sentinel Training Lab Solution listed as an installed solution.

<p align="center">
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/e40df0a397b984a9542dd1e6ab9c0907c70e4017/Images/Installing%20training%20lab%20connector.PNG" width="300" />
  <img src="https://github.com/NgethaWachira/Configuring-Microsoft-Sentinel/blob/e40df0a397b984a9542dd1e6ab9c0907c70e4017/Images/Creating%20training%20lab%20connector.PNG" width="300" />
</p>








