# escape=`

FROM microsoft/dotnet-framework:3.5-runtime-windowsservercore-1709

RUN powershell -Command Add-WindowsFeature Web-Server & `
    powershell -Command Add-WindowsFeature Web-Asp-Net & `
    %windir%\System32\inetsrv\appcmd set apppool /apppool.name:DefaultAppPool /managedRuntimeVersion:v2.0 /enable32BitAppOnWin64:true & `
    powershell -Command Remove-Item -Recurse C:\inetpub\wwwroot\* & `
    powershell -Command Invoke-WebRequest -Uri https://dotnetbinaries.blob.core.windows.net/servicemonitor/2.0.1.6/ServiceMonitor.exe -OutFile C:\ServiceMonitor.exe

EXPOSE 80

ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]
