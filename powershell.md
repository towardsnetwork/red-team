# Powershell notes
1. List all commandlets `Get-Command`
2. List of verbs
  - Get
  - Start
  - Stop 
  - Read
  - Write
  - New
  - Out
3. To get help `Get-Help`
  - `Get-Command New-*`
4. `Get-Command | Get-Member -MemberType Method`
5. Output formating
  - `Get-ChildItem | select Name`
  - `Get-ChildItem | Where-Object {$_.Name -eq "windows"}`
  - `Get-ChildItem | Where-Object -Property PropertyName -eq "windows"`
6. Sorting `Get-ChildItem | select Name | Sort-Object`
