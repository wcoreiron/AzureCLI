# AzureCLI
# Assign a principal to all resource groups
$principal = "SQL Server Admins"
$principalId = "dc3e3ec1-c670-401e-b9c5-31d4fb901df1"

# Need to filter down to those sql server instances that don't have an admin assigned
$servers = /opt/homebrew/bin/az sql server list --query "[].[name,group]" -o tsv

$servers

foreach ($server in $servers.Split([Environment]::NewLine)) { 
  Write-Host "Assigning $server"
  az sql server ad-admin create -g acura --server {server-name} -i "{principal_id}"
}
![image](https://user-images.githubusercontent.com/103061298/173436683-53b6dcf5-ae07-4a6e-a05a-ef3c4a5393c2.png)

#assing an admin to resource 
az sql server ad-admin create --display-name --object-id --resource-group --server 
