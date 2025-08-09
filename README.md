NEEDED  
IP address of the printer - should be in Glue, confirm by browsing to the printer.  
  
A name to call the Printer - this is what the printer calls itself in windows for the user eg "Main Office PR1"  
  
The driver files - download them from the manufacturers website and extract them on your compurer.  
Put the entire lot into the intunewin source directory.  
  
The filename of the driver file.  eg CNLB0MA64.inf  
  
The display name of the driver.  
  
To obtain the driver display name, you will need a Windows computer ideally with printmanagement.msc  
If it is missing - powershell as admin:  
dism /Online /add-Capability /CapabilityName:Print.Management.Console~~~~0.0.1.0  
  
Open printmanagement.msc  
Expand Print Servers  
Expand *your computer name here*  
Select Drivers  
Right click in the main window and select "Add driver..."  
Press Next twice then select "Have Disk..."  
Browse to the location that you've extracted the driver installer  
Listed here will be the available driver files eg "CNLB0MA64.inf"  
Once you select one, it will show you the display name of the driver package eg "Canon Generic Plus UFR II"  
  
----  
  
In the Source for the intunewin:  
Put the extracted contents of the driver installer AND the !printer_install.ps1 and !printer_uninstall.ps1 files  
  
----  
  
Intune Win32 installation commands  
  
Example Install command:  
powershell.exe -noprofile -executionpolicy bypass -file .\\Printer_install.ps1 -PortName "IP_10.10.1.1" -PrinterIP "10.1.1.1" -PrinterName "Canon Printer Upstairs" -DriverName "Canon Generic Plus UFR II" -INFFile "CNLB0MA64.inf"  
  
Example Uninstall command:  
powershell.exe -noprofile -executionpolicy bypass -file .\\Printer_uninstall.ps1 -PrinterName "Canon Printer Upstairs"  
  
Detection:  
Registry  
Keypath = HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Print\Printers\Canon Printer Upstairs  
Value name = Name  
Detection method = String comparison  
Operator = Equals  
Value = Canon Printer Upstairs  
