### Get installed software
Get-WmiObject -Class Win32_Product

### Get Antivirus Product Status
Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntivirusProduct

### In table format, display processes and include the CommandLine, ProcessName, and SessionID. Filter to show SessionID of 2 and ProcessName of "svchost.exe" only. Sort the results alphabetically by CommandLine.
gps | Select-Object -Property ProcessName,SessionID | Sort-Object -Property ProcessName -Descending | Where-Object SessionID -EQ 2 | Where-Object ProcessName -EQ svchost.exe | Format-Table

### Services with unquoted executable paths that start automatically can lead to escalating privileges. How many services fit that description on this machine?
Get-WmiObject -class Win32_Service -Property StartMode,PathName | Where {$_.StartMode -EQ "Auto" -and $_.PathName -notlike '"*'} | select StartMode,PathName

### Get current logged in user
query user /server:$server
Get-WmiObject -Class win32_computersystem
(Get-CimInstance -ClassName Win32_ComputerSystem).Username
(Get-WMIObject -ClassName Win32_ComputerSystem).Username


### Get file under path using hash value
Get-FileHash -Path C:\Windows\System32\* -Algorithm MD5 | findstr /i "6CECC33A62E935F5E8665B9597479A36"

### Find string in txt files under path by "password" string
Select-String -Path C:\Windows\System32\*.txt -Pattern 'password'