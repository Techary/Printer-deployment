NEEDED  
IP address of the printer.  
A name to call the Printer - this is what the printer calls itself in windows for the user.  
The driver file.  
The filename of the driver file.  
  
To obtain the driver information, download the driver installer to your computer.  
Using nanazip/7zip, extract the .exe installer.  
Use printmanagement.msc to install the driver to your computer - this way you can find out which driver file contains the driver you need, and its name.  

----

In the Source for the intunewin:
Put the extracted contents of the driver installer AND the printer_install.ps1 and printer_uninstall.ps1 files
  
----  
  
Intune Win32 installation commands  
  
Example Install command:  
powershell.exe -noprofile -executionpolicy bypass -file .\Printer_install.ps1 -PortName "IP_10.10.1.1" -PrinterIP "10.1.1.1" -PrinterName "Canon Printer Upstairs" -DriverName "Canon Generic Plus UFR II" -INFFile "CNLB0MA64.inf"  
  
Example Uninstall command:  
powershell.exe -noprofile -executionpolicy bypass -file .\Printer_uninstall.ps1 -PrinterName "Canon Printer Upstairs"  
  
Detection:  
Registry  
Keypath = HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Print\Printers\Canon Printer Upstairs  
Value name = Name  
Detection method = String comparison  
Operator = Equals  
Value = Canon Printer Upstairs  
