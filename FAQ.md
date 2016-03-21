# FAQ #

## How do I.. ##


### ...install RegRipper? ###
Go to the [download site](http://code.google.com/p/regripper/downloads/list) for RegRipper and get the archive that contains the most recent version of RegRipper (in this case, rrv2.5.zip).  Extract the archive into a directory on your system, such as "C:\rr".

Next get the latest plugin archive, based on the date of the archive, and extract everything in the archive into "C:\rr\plugins".

That's it...you're done. Either launch rr.exe (the GUI) or run rip.exe (CLI) from the command prompt.

### ...get a list of all plugins? ###

This is actually pretty straight-forward. To list all of the plugins in the \plugins folder, simply open a command prompt, navigate to the folder where you installed RegRipper, and type:

```
rip -l 
```

Another way to see what plugins are available is to launch the Plugin Browser (pb.exe), and navigate through the list of plugins, one at a time.
In order to get a .csv listing of the available plugins, use this command:

```
rip -l -c > plugins.csv
```

You can then open the resulting file in Excel.

In order to get just a listing of plugins available for a particular hive file (in this case, the Software hive), type:

```
rip -l -c | find ",Software" /i
```

## Does RegRipper do...? ##

Perhaps one of the biggest misconceptions regarding the RegRipper plugins is whether or not it **does** specific things; that is, does it check for specific values, parse specific data, or enumerate the contents of specific keys?  This isn't the right question to ask.

From the beginning, RegRipper plugins have been created and updated based on needs.  Some needs are relatively easy to meet, due to the availability of data; most Windows systems have a 'Run' key.  Other plugins have been created/modified due to unique circumstances based on analysis; finding something new or unusual during an examination will very often result in a new plugin, or an update to an existing plugin.

Of those currently writing plugins, it appears that few have encountered systems on which the P2P application Ares has been installed and used.  As such, the ares.pl plugin may be somewhat limited and not meet the complete needs of a specific examiner working on a specific case.

In short, the power of RegRipper is in the plugins, and for this to be a truly powerful tool, it depends on examiners sharing their needs and data before hand, rather than asking, "Does it do...?" after the fact.