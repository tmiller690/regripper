# Plugins #

RegRipper plugins are Perl scripts, located within the \plugins folder of your RegRipper installation, that implement the _pluginmain()_ function and extract information from a hive file.




## Plugin Descriptions ##

## attachmgr.pl ##

This plugin is intended for the NTUSER.DAT hive and gets the contents of the _Software\Microsoft\Windows\CurrentVersion\Policies\Associations_ and _Software\Microsoft\Windows\CurrentVersion\Policies\Attachments_ keys.

The plugin is intended to assist analysts with malware detection, albeit of specific samples.

[MS KB 883260](http://support.microsoft.com/kb/883260) provides an explanation of some of the values beneath these keys.  Corey Harrell provided an example of how malware uses some of these values in [this blog post](http://journeyintoir.blogspot.com/2010/10/anatomy-of-drive-by-part-2.html).

[EMDMgmt](http://windowsir.blogspot.com/2013/04/plugin-emdmgmt.html)

[FindExes](http://windowsir.blogspot.com/2013/04/plugin-findexes.html)

[MenuOrder](http://journeyintoir.blogspot.com/2013/04/plugin-menuorder.html)


[Run keys](http://journeyintoir.blogspot.com/2013/04/plugins-softrun-userrun.html) - NTUSER.DAT and Software hives

[SAMParse](http://windowsir.blogspot.com/2013/05/plugin-samparse.html) - parsing the SAM hive

[SpecAccts](http://windowsir.blogspot.com/2013/04/plugin-specacctspl.html): the functionality for this plugin has been rolled into the Winlogon plugin, and the plugin itself has been retired


[\*\_tln plugins](http://windowsir.blogspot.com/2013/04/plugin-tln.html)

[Winlogon](http://windowsir.blogspot.com/2013/04/plugin-winlogon.html)