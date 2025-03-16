# Power Shell Windows - GETS camera NTP time data and places in C:\test\pstest.txt file

$username = "admin"
$password = "123456"
$authInfo = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes("$username`:$password"))

# Camera URL
$uri = "http://admin:pppp0000@192.168.55.76/cgi-bin/configManager.cgi?action=getConfig&name=NTP""

$headers = @{"X-Requested-With"="powershell";"Authorization"="Basic $authInfo"}
[xml]$results = Invoke-Restmethod -uri $uri -headers $headers -method get

# Copies NTP time data from Dahua camera to C:\test\pstest.txt
$url2 = "http://admin:pppp0000@192.168.55.76/cgi-bin/configManager.cgi?action=getConfig&name=NTP""
$dest = "C:\test\pstest.txt"
Invoke-WebRequest -Uri $url2 -OutFile $dest

