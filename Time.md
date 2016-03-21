# Time #
This page is about how time is treated on Windows systems, as well as the various time formats found on Windows systems.

## Formats ##
Time in recorded in a number of formats on Windows systems.  Even though MS maintains [a page](http://msdn.microsoft.com/en-us/library/windows/desktop/ms724186(v=vs.85).aspx) that discusses time formats, there are other formats available, as well.

### Unix Time ###
_Unix epoch time_ - yes, there are time values recorded on Windows systems in the 32-bit [Unix epoch time](http://en.wikipedia.org/wiki/Unix_time) format, which is the number of seconds since midnight UTC, 1 Jan 1970.

This time format has a granularity of 1 second.

This time format is found in Windows XP/2003 [Event Log records](http://msdn.microsoft.com/en-us/library/windows/desktop/aa363646(v=vs.85).aspx), as well as some Registry value data.

To convert this time format to something readable, use the built-in _gmtime()_ function.

### DOSDateTime ###
_[DOSDateTime](http://msdn.microsoft.com/en-us/library/windows/desktop/ms724247(v=vs.85).aspx)_ - Date and time format encoded in two 16-bit values. Used as part of the [shell item format specification](http://download.polytechnic.edu.na/pub4/download.sourceforge.net/pub/sourceforge/l/project/li/liblnk/Documentation/Windows%20Shell%20Item%20format/Windows%20Shell%20Item%20format.pdf), described by Joachim Metz.  Shell item ID lists appear in the [Shell\BagsMRU](http://code.google.com/p/registrydecoder/source/browse/trunk/templates/template_files/ShellBagMRU.py) Registry values, as well as part of the [MS-SHLLINK binary format](http://msdn.microsoft.com/en-us/library/dd871305(PROT.10).aspx) for Windows shortcut files.

This time format has a granularity of 2 seconds.

Python code for translating the DOSDateTime values into something readable can be found as part of the [libforensics](http://code.google.com/p/libforensics/source/browse/code/lf/time.py) package.

Perl code (note: requires the Time::Local module to translate to a Unix epoch time):

```
sub convertDOSDate {
  my $date = shift;
  my $time = shift;
  if ($date == 0x00 || $time == 0x00){
    return 0;
  }
  else {
    my $sec = ($time & 0x1f) * 2;
    $sec = "0".$sec if (length($sec) == 1);
    my $min = ($time & 0x7e0) >> 5;
    $min = "0".$min if (length($min) == 1);
    my $hr  = ($time & 0xF800) >> 11;
    $hr = "0".$hr if (length($hr) == 1);
    my $day = ($date & 0x1f);
    $day = "0".$day if (length($day) == 1);
    my $mon = ($date & 0x1e0) >> 5;
    $mon = "0".$mon if (length($mon) == 1);
    my $yr  = (($date & 0xfe00) >> 9) + 1980;
    return "$yr-$mon-$day $hr:$min:$sec";
#   return gmtime(timegm($sec,$min,$hr,$day,($mon - 1),$yr));
  }
}
```

### UUID ###
_[UUID](http://www.ietf.org/rfc/rfc4122.txt)_ - Windows systems maintain volume GUIDs, particularly those associated with volumes beneath the MountedDevices and MountPoints2 keys, in [UUIDv1](http://www.ietf.org/rfc/rfc4122.txt) format.  Part of this format specification includes a 60-bit time value, which indicates the number of 100-nanosecond intervals since 15 Oct 1582 (this date is described in the RFC as _the date of Gregorian reform to the Christian calendar_).

This time format has a granularity of 100 nanoseconds.

_**Note**: This format also includes a "node" value, which for several of the volume GUIDs is a MAC address that was available on the Windows system at the time that the GUID was generated_.

### FILETIME ###
_[FILETIME](http://msdn.microsoft.com/en-us/library/windows/desktop/ms724284(v=vs.85).aspx)_ - A 64-bit time value representing the number of 100-nanosecond intervals since midnight UTC, 1 Jan 1601.  Used pervasively throughout Windows systems, and can be found:

  * $STANDARD\_INFORMATION and $FILE\_NAME attributes within MFT records
  * Registry key properties
  * Registry value data

This time format has a granularity of 100 nanoseconds.

Perl code for translating a FILETIME object into a Unix epoch time (borrowed from Andreas Schuster):

```
#-------------------------------------------------------------
# getTime()
# Translate FILETIME object (2 DWORDS) to Unix time, to be passed
# to gmtime() or localtime()
#-------------------------------------------------------------
sub getTime($$) {
  my $lo = shift;
  my $hi = shift;
  my $t;

  if ($lo == 0 && $hi == 0) {
    $t = 0;
  } else {
    $lo -= 0xd53e8000;
    $hi -= 0x019db1de;
    $t = int($hi*429.4967296 + $lo/1e7);
  };
  $t = 0 if ($t < 0);
  return $t;
}
```

### SYSTEMTIME ###
_[SYSTEMTIME](http://msdn.microsoft.com/en-us/library/windows/desktop/ms724950(v=vs.85).aspx)_ - 128-bit format, and according to MS, "_The time is either in coordinated universal time (UTC) or local time, depending on the function that is being called._"  This time format is used in a number of artifacts on Windows systems, including (but not limited to) in XP Scheduled Task/.job files, as well as in value data beneath the Vista/Win7 NetworkList key (within the Software hive).

It is important to note that this value can be stored in the Registry in either UTC or localtime format.  Beneath the NetworkList key, for example, the value is stored in localtime format.

This time format has a granularity of 1 millisecond.

Example Perl code to parse this date format appears as follows:

```
sub parseDate128 {
  my $date = $_[0];
  my @months = ("Jan","Feb","Mar","Apr","May","Jun","Jul",
	              "Aug","Sep","Oct","Nov","Dec");
  my @days = ("Sun","Mon","Tue","Wed","Thu","Fri","Sat");
  my ($yr,$mon,$dow,$dom,$hr,$min,$sec,$ms) = unpack("v*",$date);
  $hr = "0".$hr if ($hr < 10);
  $min = "0".$min if ($min < 10);
  $sec = "0".$sec if ($sec < 10);
  my $str = $days[$dow]." ".$months[$mon - 1]." ".$dom."
     ".$hr.":".$min.":".$sec." ".$yr;
  return $str;
}
```

### Strings ###
_Strings_ - Date and time values may be stored in Registry value data in string format; ie, "2011-06-07" or "1/2/2011".  This is often found in Registry values in specific applications.

To convert data stored in this format to a Unix epoch time, parse the strings and use the _Time::Local_ module to convert the information.

## File System Tunneling ##
MS [KB172190](http://support.microsoft.com/kb/172190) describes file system tunneling, which can have a significant impact on your analysis.

# Links #
MS [KB299648](http://support.microsoft.com/kb/299648): Description of NTFS date and time stamps

MS: [File Times](http://msdn.microsoft.com/en-us/library/windows/desktop/ms724290%28v=vs.85%29.aspx)

MS [KB188768](http://support.microsoft.com/kb/188768): Working with the FILETIME structure

MS: [SYSTEMTIME structure](http://msdn.microsoft.com/en-us/library/windows/desktop/ms724950%28v=vs.85%29.aspx)

MS: [DosDateTimetoFileTime function](http://msdn.microsoft.com/en-us/library/windows/desktop/ms724247%28v=vs.85%29.aspx)

Software Sleuthing: [DateTime formats and conversions](http://blogs.msdn.com/b/joshpoley/archive/2007/12/19/date-time-formats-and-conversions.aspx)

Old New Thing Blog: [DateTime formats and conversions](http://blogs.msdn.com/b/oldnewthing/archive/2003/09/05/54806.aspx)