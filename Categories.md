# Categories #
This pages presents and discusses a list of artifact categories, as they relate to the RegRipper tools and plugins.  As they are defined or described (see below), each of these categories applies specifically to artifacts found within the Windows Registry.

Many of the available Registry artifacts persist beyond file and program deletion, providing indications of system or user activity that occurred in the past.

Many artifacts can and may fall within multiple categories.  For example, the File Access category by extension indicates Program Execution.

Multiple categories of artifacts can be used in analysis though the use of an analysis matrix.

Categories are identified within plugins as part of the configuration hash (_%config_) provided as part of the plugin.  The use of categories in this manner does not obviate the use of profiles within RegRipper; instead, it enhances that capability.

**Note**: This should be considered to be a living document, subject to update and modification.

# Category Definitions #
What follows are some of the categories that have been identified, along with descriptions of each of the categories.

Where applicable, examples of available RegRipper plugins are provided.

## OS Info ##
Basic OS information, such as version, installation date, install source path, time zone information, etc.

_Example plugins:_ winver.pl, compname.pl

## User Account Info ##
Basic user account information.

_Example plugins:_ samparse.pl, profilelist.pl

## Network Configuration ##
Artifacts associated with the network configuration of the system.

_Example plugins:_ compname.pl, networklist.pl

## AutoStart ##
Registry artifacts associated with the autostart of applications and programs (those programs/applications that are launched with no interaction from the user or system).

This category can overlap with and include some of the same artifacts as those from the Program Execution category.

_Example plugins:_ services.pl, legacy.pl

## Program Execution ##
Artifacts that relate to or indicate that programs were executed.

_Example plugins:_ appcompatcache.pl, direct.pl, sysinternals.pl, muicache.pl, userassist.pl

## Installed Programs ##
Installed Programs artifacts differ from Program Execution artifacts, in that many applications/programs are installed on a Windows system via a setup.exe file, or via an MSI file.  As such, the program itself has artifacts in the Software hive, and then user-specific artifacts "live" in the user's NTUSER.DAT hive.

An example of this includes Adobe Reader; the Software hive will contain information about the system-wide application configuration, while the NTUSER.DAT hives will indicate not only which user(s) launched the application, but also maintain an MRU list of files that the user accessed.

Note: A program or application can be installed, but may not have been executed.

_Example plugins:_ apppaths.pl

## Storage Information ##
This category pertains to the usage of or access to storage media, including (but not limited to) USB devices, network shares, "cloud" storage, etc.

_Example plugins:_

## Log Info ##
This category pertains to artifacts related to the configuration of log files on the system, which can include Windows Event Logs, as well as application specific logs.

_Example plugins:_

## Malware ##
This category pertains to artifacts that specifically provide indications of malware infection or activity.  This category differs from the AutoStart category, in that legitimate applications can make use of AutoStart artifacts.  In many instances, the AutoStarts or Program Execution categories can be used to extract general information (i.e., contents of the Run key, etc.) that the analyst can review, plugins in the Malware category can be used to look for specific artifacts related to a variety of specific malware samples, or related to malware families.

Examples of a malware specific artifacts include:
  * Variants of Zeus have been known to add "sdra64.exe" to the UserInit Registry value
  * OSVerion

_Example plugins:_ osversion.pl, zeus.pl

## File Access ##
This category pertains to files that a user has accessed, which is most often through the use of a specific application.  As such, artifacts within this category will indicate Program Execution (or usage), but the purpose of this category is to provide indications of files that a user specifically had access to, via downloading, or through creation or modification.

_Example plugins:_ recentdocs.pl, trustrecords.pl

## Communications ##
This category can be a subset of the Installed Programs and Program Execution categories, and is specific to programs/applications intended for off-system communications.  While the Program Execution category may be used to look for indications of the use of ftp.exe or chat programs, this category is intended for communication application-specific artifacts.

_Example plugins:_

# Analysis Matrix #
The above listed categories can be used in an analysis matrix; several categories of artifacts may be used in specific types of analysis activities.

The following table is a notional analysis matrix, and is intended to serve as a starting point for both discussion and analysis:

| |Malware Detection|Data Exfil|Unauth Use|Illicit Images|
|:|:----------------|:---------|:---------|:-------------|
|Program Execution|X                |          |          |X             |
|Malware|X                |          |          |X             |
|File Access|                 |X         |          |X             |
|Storage Info|                 |X         |          |X             |
|Comms|X                |X         |          |              |