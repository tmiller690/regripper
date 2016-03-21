# Introduction #

This Wiki page outlines the common Auto-Start Extensibility Points (ASEPs) leveraged by attackers and malware to remain persistent on a Windows system. For each ASEPs the RegRipper plug-in that checks the auto-start location is highlighted.

# Details #

**Run Keys**

_Software Hive Run keys_

• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Terminal Server\Install\Software\Microsoft\Windows\CurrentVersion\Runonce

• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Terminal Server\Install\Software\Microsoft\Windows\CurrentVersion\Run

• HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

• HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run

• HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce

• HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\RunOnce

• HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run

• HKLM\Software\ Microsoft\Windows\CurrentVersion\RunServices

• HKLM\Wow6432Node\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run

• soft\_run plugin

_NTUSER.DAT Hive Run keys_

• HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows\Run

• HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run

• HKCU\Software\Microsoft\Windows\CurrentVersion\Run

• HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce

• HKCU\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Terminal Server\Install\Software\Microsoft\Windows\CurrentVersion\Runonce

• HKCU\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Terminal Server\Install\Software\Microsoft\Windows\CurrentVersion\Run

• HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\RunServices

• HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\RunServicesOnce

• HKCU\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Run

• HKCU\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run

• HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows

> o Run and Load values

• user\_run plugin


**System Services**

• HKLM\System\CurrentControlSet\Services

> o services plugin (list services by last write times)

> o svcdll plugin (list services with ServiceDLL values)

> o svc plugin to (list services and drivers by last write times)

> o svc\_plus plugin (short format with warnings for type mismatches)

> o svc2 plugin (csv output)

• Legacy registry keys located at HKLM\System\CurrentControlSet\Enum Root

> o legacy plugin


**Software Registry Hive ASEPs**

• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit
> o winlogon plugin
• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell
> o winlogon plugin
• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Taskman
> o winlogon plugin
• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\System
> o winlogon plugin
• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
> o winlogon plugin
• HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\SpecialAccounts\UserList
> o winlogon plugin
• HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components
> o installedcomp plugin
• HKLM\SOFTWARE\Wow6432Node\Microsoft\Active Setup\Installed Components
> o installedcomp plugin
• HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellExecuteHooks
> o shellexec plugin
• HKLM\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellExecuteHooks
> o shellexec plugin
• HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
> o bho plugin
• HKLM\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
> o bho plugin
• HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
> o drivers32 plugin
• HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
> o drivers32 plugin
• HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options
> o imagefile plugin
• HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Image File Execution Options
> o imagefile plugin
• HKLM\SOFTWARE\Classes\Exefile\Shell\Open\Command\(Default)
> o cmd\_shell plugin
• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows\Appinit\_Dlls
> o appinitdlls and init\_dlls plugins
• HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Windows\Appinit\_Dlls
> o appinitdlls plugins
• HKLM\SOFTWARE\Microsoft\SchedulingAgent
> o schedagent plugin
• HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell Extensions\Approved
> o shellext plugin
• HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SvcHost
> o svchost plugin


**System Registry Hive ASEPs**

• HKLM\System\CurrentControlSet\Control\Session Manager\AppCertDlls
> o appcertdlls plugin
• HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SecurityProviders
> o securityproviders plugin
• HKLM\SYSTEM\CurrentControlSet\Control\Lsa\Authentication Packages
> o lsa\_packages plugin
• HKLM\SYSTEM\CurrentControlSet\Control\Lsa\Notification Packages
> o lsa\_packages plugin
• HKLM\SYSTEM\CurrentControlSet\Control\Lsa\Security Packages
> o lsa\_packages plugin
• HKLM\SYSTEM\ControlSet00.$current.\Control\Session Manager\CWDIllegalInDllSearch
> o dllsearch plugin
• HKLM\SYSTEM\ControlSet00.$current.\Control\SafeBoot
> o safeboot plugin


**NTUSER.DAT Registry Hive ASEPs**

• HKCU\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell
> o winlogon\_u plugin
• HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows\Load
> o load plugin
• HKCU\Software\Microsoft\Command Processor\Autorun
> o cmdproc plugin


**UsrClass.dat Registry Hive ASEPs**

• HKCU\Classes\Exefile\Shell\Open\Command\(Default)
> o cmd\_shell\_u plugin