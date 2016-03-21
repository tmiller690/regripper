# ShellBags #



MS [KB 813711](http://support.microsoft.com/kb/813711) describes what actions cause data to be added to the Shell Bags values.

The structure of shell items is very important to understand, as these structures are used in multiple locations on Windows systems, not just in the Shell BagMRU subkeys within the Registry.  For example, the structures are used in the shell item ID list section in Windows shortcut [LNK](http://msdn.microsoft.com/en-us/library/dd871305%28v=prot.13%29.aspx) files, as well as within the LNK streams in .automaticDestinations-ms Jump List files on Windows 7.  These structures are also used within the data of values beneath the OpenSavePidlMRU keys within the Windows 7 NTUSER.DAT hives (full path is "HKU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU").

As such, being able to recognize and parse these structures is essential to being able to fully understand the data that you're looking at, and what it's telling you.


### GUIDs ###
The Variable type (type == 0x00) data structures can contain a variety of information, in various formats.  One of the data structures, in particular, can be seen (when viewed in hex) to contain "1SPS" in several places.  If the data is broken up, using "1SPS" as a separator (ie, via Perl's _split()_ function), the first 16 bytes of each section appears to be a GUID.

One GUID in particular appears as follows:

{B725F130-47EF-101A-A5F1-02608C9EEBAC} - Ref: [Schema (Windows)](http://msdn.microsoft.com/en-us/library/aa965725%28v=vs.85%29.aspx)

Apparently, this GUID applies to both desktop and Metro-style (Win8) apps, and is referred to as both a [SHCOLUMNID](http://msdn.microsoft.com/en-us/library/windows/desktop/bb759748(v=vs.85).aspx) and a [PROPERTYKEY](http://msdn.microsoft.com/en-us/library/windows/desktop/bb773381(v=vs.85).aspx) structure.  The contents of the subsection of data that begins with this GUID can be further parsed using a distinct set of rules.


## References ##

MS: [Canonical Names of Control Panel Items](http://msdn.microsoft.com/en-us/library/windows/desktop/ee330741%28v=vs.85%29.aspx)

MS: [Known Folder GUIDs](http://msdn.microsoft.com/en-us/library/bb882665.aspx)

MS: [KnownFolderID](http://msdn.microsoft.com/en-us/library/windows/desktop/dd378457%28v=vs.85%29.aspx)


## Links ##
Joachim Metz's [Windows Shell Item format specification](http://download.polytechnic.edu.na/pub4/download.sourceforge.net/pub/sourceforge/l/project/li/liblnk/Documentation/Windows%20Shell%20Item%20format/Windows%20Shell%20Item%20format.pdf) paper (PDF)

[ShellBagMRU.py](http://code.google.com/p/registrydecoder/source/browse/trunk/templates/template_files/ShellBagMRU.py), part of Registry Decoder (written by Kevin Moore)

Willi Ballenthin's [Windows Shellbag Forensics](http://www.williballenthin.com/forensics/shellbags/index.html)