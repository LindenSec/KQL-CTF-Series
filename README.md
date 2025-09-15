# KQL CTF #1 Datasets (Synthetic)

Tables:
- SigninLogs.csv
- DeviceProcessEvents.csv
- CommonSecurityLog.csv

## Ingest into Azure Data Explorer Free Cluster

1) Create tables (run in ADX query window):

.create table SigninLogs (TimeGenerated: datetime, UserPrincipalName: string, IPAddress: string, ResultType: string, Role: string)
.create table DeviceProcessEvents (TimeGenerated: datetime, DeviceName: string, AccountName: string, FileName: string, ProcessCommandLine: string, InitiatingProcessFileName: string)
.create table CommonSecurityLog (TimeGenerated: datetime, DeviceName: string, SourceIP: string, DestinationIP: string, DestinationHostName: string)

2) Ingest CSVs:
- In the left panel, choose the database → **Ingest new data** → pick table → upload CSV.
- Ensure the column headers match exactly.

3) Time range:
- Data covers the last ~48 hours relative to generation time (UTC).
- For hunts, start with: `| where TimeGenerated > ago(48h)`.

## Notes
- The data includes mostly benign activity, with a single malicious chain:
  password-spray → admin success → PowerShell → download → exfil to a rare domain.
- Flags are present in the data (not listed here).

© LindenSec synthetic data for educational use.
