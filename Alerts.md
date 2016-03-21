# Alerts #
The purpose of adding alerts (or an alerting function, via _alertMsg()_) is to provide a facility for identifying items of interest (from previous analyses) within the vast wealth of data available within a Windows system, and in particular the Registry.  This allows an analyst to identify "low-hanging fruit" that may be of value to an examination.

This page will serve as a facility for collaboration amongst the admins of this site, to add, revise, and hone the information alerted on within various plugins.

## Plugins ##

Many plugins provide path information that can be searched via _grep()_ for specific indicators of suspicious or malicious activity:

  * appcompatcache.pl
  * userassist.pl
  * service.pl - also, added Beth S.'s checks from svc\_plus.pl to the services.pl plugin


_Note:_ To avoid issues with case sensitivity, process the path through the _lc()_ function first, and then grep for the lower-case string of interest.

## Paths ##
Below are some paths to check for:

  * Recycle
  * GlobalRoot
  * System Volume Information
  * App + Data (gets "Application Data", and "AppData")
  * Temp
  * ADSs - _split()_ the path, check the final element for a colon

_Example Code_:
```
my @vals = ("Recycle","GLOBALROOT","System Volume Information", "Temp",
  "Application Data","AppData");

foreach my $v (@vals) {
  ::alertMsg("ALERT: ".$v." found in path: ".$_) if (grep(/lc($v)/,lc($_));
}
```

_Example ADS Check_:
```
my @vals = split(/\\/,$_);

my $int = scalar(@vals) - 1;

::alertMsg("ALERT: Possible ADS found: ".$_) if (grep(/:/,$vals[$int]));

```

## Other Checks ##

  * appinitdlls.pl - generate an alert if the value is NOT blank
  * imagefile.pl - generate an alert if a Debugger value is found
  * attachmgr.pl - generate an alert based on MS [KB 883260](http://support.microsoft.com/kb/883260)
  * winlogon.pl - generate several alerts; UserInit value with multiple entries, 'TaskMan', 'System, 'load' or 'run' values found, etc.


## Checking for Encryption ##

  * MountedDevices key - check value data for "TrueCryptVolume"; access to a TrueCrypt volume often results in a volume GUID within the MountedDevices key that includes "TrueCryptVolumeN" in the data (with N being a volume letter)