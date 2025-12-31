# Microsoft-Azure-Sentinel-XDR-Mini-Project-1

## Objective

To build a simulated SOC environment using Microsoft Azure, Microsoft Sentinel, Microsoft Defender XDR, and a Windows 11 virtual machine. This project demonstrates my ability to deploy cloud resources, ingest logs, configure security tools, create dashboards, and generate alerts for investigation. The goal was to understand how Microsoft’s security ecosystem works end‑to‑end — from log ingestion to alerting to investigation.

### Skills Learned


- Setting up a cloud‑based SOC environment using Azure, Sentinel, and Defender XDR
- Creating and configuring Azure resources (subscriptions, billing, resource groups, virtual machines)
- Ingesting logs into Microsoft Sentinel and Microsoft Defender XDR
- Understanding how Azure Activity Logs, endpoint logs, and training logs flow into XDR
- Building dashboards and visualizations using Workbooks and KQL queries
- Writing beginner‑friendly KQL queries for log analysis and alert creation
- Creating scheduled analytics rules to generate alerts based on log patterns
- Bookmarking suspicious events for future investigation
- Strengthening SOC workflow fundamentals: deploy → ingest → analyze → alert → investigate
- Improving documentation and project planning using diagrams and structured steps


### Tools Used

- Microsoft Azure – resource creation, VM deployment, subscription management
- Microsoft Sentinel – log ingestion, KQL queries, dashboards, analytics rules
- Microsoft Defender XDR – alert context, device timeline, Azure Activity ingestion
- Windows 11 Virtual Machine – endpoint log generation and testing
- Log Analytics Workspace – central log storage and query engine
- KQL (Kusto Query Language) – searching and visualizing cloud telemetry
- CyberChef – decoding and quick data analysis
- VirusTotal – validating URLs, files, and hashes
- Notepad++ – documentation and note‑taking
- draw.io – project diagramming and workflow mappin


## Steps

# Project Summary

In this project I create a Microsoft Account, Azure, Microsoft XDR, and Windows 11 virtual machine and ingest the logs into XDR for investigation or tracking logs. After creating the foundation of a simulated SOC environment I set up training logs, create a dashboard, ingest logs, create alert and bookmark logs for future investigation.  

# Project Diagram

Utilized [draw.io](http://draw.io) to create overview of the project. This will help me map out the project which will create a step by step process so I won’t deviate from the project or manage many tasks.

network map
<img width="1049" height="972" alt="image" src="https://github.com/user-attachments/assets/9dfb7623-691c-42b4-9e54-1963996050a1" />


# Overview Steps

Create Microsoft Azure Account

Setup Billing

Create Windows Virtual Machine

Setup Log Workspace

Setup Microsoft Sentinel

Setup Microsoft XDR

Ingest Training Logs

Create Workbook

Connect Microsoft XDR to Sentinel

Create Alerts

Create Bookmarks

# Create Microsoft Azure Account

Head over to https://www.microsoft.com/en-us/microsoft-365/enterprise/office-365-e5?activetab=pivot:overviewtab register for account to subscribtion. This subscription allow for Microsoft Endpoints, Office to utilized for Microsoft Sentinel. Without the subscription you cannot ingest logs from endpoints and office.

Setup 2MFA for Microsoft login process. There are different platforms to manage your subscribtions so knowing what each provides will help you manage your usage and systems.

- [admin.microsoft.com](http://admin.microsoft.com)
    - This link help manage Users, Groups, Billing and Marketplace apps.
    - Sign up for Microsoft 365E5 (no team trial)
    - Assign license Microsoft 365E5 to your user
    - Currently there are 88 apps with this subscription
        - Microsoft 365 Defender
        - Microsoft 365 for Endpoint
        - Microsoft 365 for Office
        - Many more…

<img width="1109" height="428" alt="image" src="https://github.com/user-attachments/assets/d2787cfb-11ec-434f-aa24-4343694bb2cd" />

<img width="1102" height="214" alt="image" src="https://github.com/user-attachments/assets/cbf9b571-4a82-48cd-ba7e-b1e313f2f3fc" />

<img width="1080" height="636" alt="image" src="https://github.com/user-attachments/assets/a31f1d85-9867-44b0-a340-60a97495dd4d" />

<img width="1031" height="858" alt="image" src="https://github.com/user-attachments/assets/2469576c-6f19-4612-b9cc-1920cf5c4961" />

<img width="599" height="297" alt="image" src="https://github.com/user-attachments/assets/d46e6106-09ef-4547-9fad-6c6f45dd00a0" />



Create Azure account [portal.azure.com](http://portal.azure.com). 

<img width="1099" height="198" alt="image" src="https://github.com/user-attachments/assets/f1121017-3a62-4f1a-971f-a74571be3183" />


# Setup Billing

In `product` , `Microsoft 365 E5 ( no Teams )` change Recurring billing if you are testing but you need a subscription to add other features. 

<img width="1100" height="454" alt="image" src="https://github.com/user-attachments/assets/f4bb3869-d2bf-423b-b64f-8a8a19a3ea00" />


On [http://portal.azure.com](http://portal.azure.com/) manage your cost and billing. At the top search for `cost management + billing` 

<img width="1098" height="344" alt="image" src="https://github.com/user-attachments/assets/3c2d5491-7aa1-4b65-9c39-2236163a1d7d" />


On the navigation bar on the left click on `Monitoring`, `Budgets` to add your budget to get alerts if it reach a certain amount. 

<img width="1099" height="633" alt="image" src="https://github.com/user-attachments/assets/a9a9978f-4fe8-4ed7-aff3-3e7d0769163e" />


<img width="1096" height="1300" alt="image" src="https://github.com/user-attachments/assets/dfab1a9e-3c8c-4005-adbf-1742357cef3f" />

<img width="1101" height="308" alt="image" src="https://github.com/user-attachments/assets/e56327f2-cbea-4bff-820b-f9f156c7dd3d" />


# Create Windows Virtual Machine

On Azure search for `resource groups` to group resources in one place. 

<img width="591" height="193" alt="image" src="https://github.com/user-attachments/assets/c9c91546-70fb-4f9c-b55f-cc97c208b808" />


<img width="1108" height="330" alt="image" src="https://github.com/user-attachments/assets/4a644ba7-9ed6-454c-ac40-0b16d90d70c4" />


Create Windows Virtual machine, in the search bar type Virtual Machine. Create virtual machine make sure to choose the resource group you created and location/region to be the same so your virtual machine are connected in the same location/region or you will not be able to connect your resources together. 

For image you can choose Window 11 and choose your size or hardware setting, NIC, and RDP.

Once your virtual machine is setup and deployed make sure to edit your firewall rule so only you can access the machine and no one else. 

On the left Navigation bar choose Networking, Network Setting and change the RDP to only allow your IP Address.

Test RDP to your cloud Windows 11 machine. On you computer search for RDP and connect your virtual machine with the IP address and sign in using your user name and password you create for this virtual machine. 

<img width="594" height="185" alt="image" src="https://github.com/user-attachments/assets/d63f6c57-3d62-4481-bc3c-f98f02dd68c6" />


<img width="594" height="278" alt="image" src="https://github.com/user-attachments/assets/15378a82-d3da-47a0-af17-dd1bfb6e14a1" />


<img width="1099" height="953" alt="image" src="https://github.com/user-attachments/assets/cafeed93-ee96-4491-ab75-a43e15783a6a" />


<img width="1103" height="660" alt="image" src="https://github.com/user-attachments/assets/a6858765-c760-43e0-acee-c47424f760ea" />


<img width="1101" height="308" alt="image" src="https://github.com/user-attachments/assets/03e10d4e-4a60-42a1-af9d-8819f9fcfd05" />


<img width="1105" height="457" alt="image" src="https://github.com/user-attachments/assets/dd1d82ff-843e-4251-8a0b-fbdad9d902ba" />


<img width="1086" height="501" alt="image" src="https://github.com/user-attachments/assets/1c77dc0d-5158-4ebb-99b1-3d3593dc3dac" />


<img width="625" height="348" alt="image" src="https://github.com/user-attachments/assets/781a6554-ee0c-45ac-be58-0ccec32cab68" />


# Setup Log Workspace

In the search bar search for `Log Analytics Workspaces` and `+ Create` . When creating Log Analytics make sure to have resource in the resource you have created.

Once you fill out the information your deployment should be completed and ready to start ingesting from endpoints. 

<img width="1108" height="459" alt="image" src="https://github.com/user-attachments/assets/cf5b1486-bef4-485d-99ec-ddfba74db458" />


<img width="1109" height="447" alt="image" src="https://github.com/user-attachments/assets/5e32dd19-437e-42fa-946a-27cd94b529c1" />


<img width="1132" height="838" alt="image" src="https://github.com/user-attachments/assets/5f26b647-28e8-4776-84cc-acc5888ff3e6" />


# Setup Microsoft Sentinel

Setting up Microsoft Sentinel, on the search bar search for Microsoft Sentinel. `+ Create` Sentinel and you should see the Log Analytics Workspace you just create. This will pull the logs into Sentinel for future investigation. As of November 15, 2025 Microsoft Sentinel is migrating to Microsoft XDR, this is where you will do your advance searches. This will take some time to get setup before you can start utilizing the platform. 

<img width="1101" height="517" alt="image" src="https://github.com/user-attachments/assets/729f9594-9604-430d-aca3-be38273db8d9" />


<img width="1050" height="985" alt="image" src="https://github.com/user-attachments/assets/cb8a6941-adb7-45d9-ac84-153da2e72d83" />


<img width="1102" height="704" alt="image" src="https://github.com/user-attachments/assets/d668ed66-b32f-4a0e-ad6e-fa9b68412c96" />


# Setup Microsoft XDR

In this section we are going to send the activity logs from Azure to Microsoft XDR as Microsoft is migrating over from Sentinel to XDR.  For sending Azure Logs to XDR to do http://portal.azure.com search for `Subscriptions` and choose your `Azure Subscription` and click on `Activity Log` on left navigation bar. Then you are going to `Export Activity Logs` to XDR.

Now your Azure activity will be sent to Microsoft XDR.

<img width="1098" height="272" alt="image" src="https://github.com/user-attachments/assets/c1e38f3a-39af-4cc5-8903-aaa37b2e65c5" />

<img width="1106" height="388" alt="image" src="https://github.com/user-attachments/assets/3e6ce0ca-ccbe-4af5-a284-5dbac5a43fb1" />


<img width="1108" height="323" alt="image" src="https://github.com/user-attachments/assets/74d8e475-0994-45cd-82a2-369ffb534799" />

<img width="1101" height="719" alt="image" src="https://github.com/user-attachments/assets/c87bd9b8-b9b3-4d02-94d6-87bf28625340" />


Head over to https://security.microsoft.com/ to log in to Microsft XDR. This is where you will install Azure Activity under `Microsoft Sentinel` > `Content Management` > `Content Hub` > search for `Azure Activity` and install. 

<img width="1091" height="828" alt="image" src="https://github.com/user-attachments/assets/72faa4f7-eb14-4193-9234-16e49c18f136" />


# Ingest Microsoft Training Logs

Work around as of November 15, 2025 you will have to go to https://portal.azure.com/ to install `Microsoft Sentinel Training Lab Solution`.  Search for `Microsoft Sentinel Training Lab Solution` and choose resource group you have created earlier and create the `Microsoft Sentinel Training Lab Solution` logs to Microsoft XDR. This will take sometime in ingest into Microsoft XDR. 

<img width="1097" height="538" alt="image" src="https://github.com/user-attachments/assets/1f1eac1e-f941-4a62-a9d8-27a9b15ed34a" />

<img width="1084" height="882" alt="image" src="https://github.com/user-attachments/assets/013cfdad-13d4-4ea9-8b52-d65e0f4ba584" />

<img width="1110" height="567" alt="image" src="https://github.com/user-attachments/assets/463e4768-4cad-4fae-8131-1c7f551cf3c6" />


# Create Workbook

In this section you are going to create a Workbook to create Dashboards. On the navigation bar choose `Microsoft Sentinel` > `Threat management` > `Workbooks` > + `Add Workbook` > `edit` > `+ Add` > `Add data + Visualization`.

<img width="1094" height="1141" alt="image" src="https://github.com/user-attachments/assets/634064cc-2386-4c35-bf7d-45677dab86da" />


<img width="1100" height="513" alt="image" src="https://github.com/user-attachments/assets/bfae2b83-6bf7-4a25-a42a-7dff8eb9c6f0" />


<img width="607" height="1073" alt="image" src="https://github.com/user-attachments/assets/313035c2-9ee4-4669-9f1a-ee2268dba98e" />


When adding data source you can create a KQL query to get data and choose the Visualization option to change the data into a (Bar Chart, Pie, ect..) In this case I am looking for security event that with `top 5 failed login` and `Schedule Task Deleted` in a visual for my dashboard. This events are from the Microsoft Sentinel Training Logs that you have just imported in earlier. 

```jsx
SecurityEvent_CL
| where EventID_s == "4625"
| summarize Count = count() by Account_s
| sort by Count  
| take 5
```

<img width="1090" height="1088" alt="image" src="https://github.com/user-attachments/assets/ca037974-f034-4c4f-aaf3-49d5026f09d7" />

<img width="1104" height="957" alt="image" src="https://github.com/user-attachments/assets/3a979dc2-3cf2-4c8e-978a-d5b4543c8182" />


<img width="1102" height="876" alt="image" src="https://github.com/user-attachments/assets/17372a52-7b07-4ed2-b2e3-77794461901a" />


<img width="1104" height="1213" alt="image" src="https://github.com/user-attachments/assets/ace882bb-971d-4493-9e9e-9dfab66277a6" />


# Connect Microsoft XDR to Sentinel

In this section we are going to connect XDR to Sentinel so all your endpoint are sending log. Head over to https://security.microsoft.com/ just like the Azure Activity installation we are going to search for Microsoft XDR and install it. Once you install you should have Azure Activity and Microsoft XDR installed, to check you can 

In Microsoft XDR open connectors and you can import the options available but in this case I want to limit the options to AlertInfo and AlertEvidence.  

<img width="1099" height="868" alt="image" src="https://github.com/user-attachments/assets/d4fe7f90-7318-44e5-9e87-41a93f8790c4" />

<img width="1093" height="861" alt="image" src="https://github.com/user-attachments/assets/ffab6094-b735-488a-9e08-17b54d7b14d4" />


<img width="1095" height="859" alt="image" src="https://github.com/user-attachments/assets/c316edcd-56fc-4806-99bd-550f0ab26852" />


# Create Alerts

In this section I want to create an alert so when a log matches the KQL query it will send a alert for you to investigate. On left side navigation bar in Microsoft XDR under `Microsoft Sentinel` > `Configuration` > `Analytics`, this is where we will create alert rule. 

Click on + Create > Schedule query rule. This is where you will create the KQL and save the alert.  In this alert I am creating a KQL query looking for Failed Log-ons. This is set to run every 5 min to test the alert. You can change this alert to every 24hour or so after testing the alert or to your organization policy. 

```jsx
SecurityEvent_CL
| where EventID_s == "4625"
| summarize FailedLogons = count() by Account_s
| where FailedLogons >= 1000
| sort by FailedLogons desc

```

Run query every 5 minutes > 24 hours > Start running “Automatically” > greater than 0 > Group all events into a single alert > Next: > Incident setting “ Enabled” > Next > Next > Save

<img width="1102" height="866" alt="image" src="https://github.com/user-attachments/assets/f3c04821-e363-4a39-8ec3-168720ebe612" />


<img width="1093" height="842" alt="image" src="https://github.com/user-attachments/assets/d261a294-8ddf-4db7-b2d4-1a9f26213f8d" />


<img width="1099" height="777" alt="image" src="https://github.com/user-attachments/assets/c237a1c1-fa2b-46a5-a65b-3e36448f889b" />


Next, head over to Investigation & Response > Incidents & alerts > Alerts to see if the alert works. In this case the alert works and allows you to investigate further. 

<img width="1099" height="1209" alt="image" src="https://github.com/user-attachments/assets/e5e5c9e7-78f6-4140-ab97-2874763c7158" />


# Create Bookmarks

In this section we are going to use the Microsoft Sentinel Training Logs to investigate and create bookmark for future investigation as we have not yet have any logs for the Window Virtual Machine. On [azure.microsoft.com](http://azure.microsoft.com) Head over to Microsoft Sentinel and under logs create a KQL and search for any suspecting logs to bookmark for future investigation. 

In this book mark I was looking at the Office Activity to see if I can see any suspecting logs. I found that there a lot of IP address that was the same accessing a sharepoint but one IP address was different. I checked that log and choose bookmark to save it for future investigation with notes. 

 

<img width="1095" height="671" alt="image" src="https://github.com/user-attachments/assets/27414c76-da31-4beb-9fcf-5fc9de2a043b" />


<img width="1090" height="796" alt="image" src="https://github.com/user-attachments/assets/fae4f484-20fd-473f-8ef5-867b4c114454" />


<img width="564" height="1658" alt="image" src="https://github.com/user-attachments/assets/15ecbe54-650d-4a4a-b638-ef9d1257a880" />


Back on Microsoft Defender > Microsoft Sentinel > Threat Management > Hunting > Bookmark. This is where you can see the bookmark with notes and investigate further. 

<img width="1104" height="760" alt="image" src="https://github.com/user-attachments/assets/176ec06a-0f32-4dc9-b0d4-9fda7024c4fb" />


<img width="578" height="1656" alt="image" src="https://github.com/user-attachments/assets/b0f67faa-bdaf-44b0-81f4-5e5312f4448b" />


<img width="1099" height="424" alt="image" src="https://github.com/user-attachments/assets/e8697da0-e3ae-46ac-92ce-91737d7e7ba5" />


Once you evaluate the bookmark you can assign the investigation to yourself or another user.

<img width="1099" height="709" alt="image" src="https://github.com/user-attachments/assets/18f7ab63-ba5c-438d-a4f8-c2d6f9d79987" />

<img width="1070" height="609" alt="image" src="https://github.com/user-attachments/assets/9f600280-3007-429a-ab3c-5ec617c24347" />


<img width="1080" height="445" alt="image" src="https://github.com/user-attachments/assets/b5c8bed0-cc00-447c-b80c-53298e069dfe" />

<img width="1052" height="486" alt="image" src="https://github.com/user-attachments/assets/6cb52af0-a9ba-4258-8af3-58b40c600495" />

<img width="1085" height="334" alt="image" src="https://github.com/user-attachments/assets/f12d633b-7419-4bba-8c86-5e3549499cf5" />

