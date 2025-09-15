# KQL CTF #1 Datasets (Synthetic)

Tables:
- SigninLogs.csv
- DeviceProcessEvents.csv
- CommonSecurityLog.csv

## Ingest into Azure Data Explorer Free Cluster

Start by creating a free cluster over at https://aka.ms/kustofree

1) Create tables (run in ADX query window):

.create table SigninLogs (TimeGenerated: datetime, UserPrincipalName: string, IPAddress: string, ResultType: string, Role: string)

.create table DeviceProcessEvents (TimeGenerated: datetime, DeviceName: string, AccountName: string, FileName: string, ProcessCommandLine: string, InitiatingProcessFileName: string)

.create table CommonSecurityLog (TimeGenerated: datetime, DeviceName: string, SourceIP: string, DestinationIP: string, DestinationHostName: string)

2) Ingest CSVs:
- In the left panel, choose the database → **Ingest new data** → pick table → upload CSV.
- Ensure the column headers match exactly.


## Notes
- The data includes mostly benign activity, with a single malicious chain:
  password-spray → admin success → PowerShell → download → exfil to a rare domain.

© LindenSec synthetic data for educational use.
