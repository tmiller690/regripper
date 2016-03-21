# Update History #

## 20130429 ##
  * created winlogon\_tln.pl, applets\_tln.pl
  * added alertMsg() func. to:
    * brisv.pl, inprocserver.pl, inprocserver\_u.pl, iejava.pl, spp\_clients.pl
  * retired scanwithav.pl (func. included in attachmgr.pl)
  * retired taskman.pl (func. included in winlogon.pl)
  * retired vista\_wireless.pl (func. in networklist.pl)

## 20130425 ##
  * RegRipper and rip updated to v2.8; added alertMsg() capability
  * retired userinit.pl (functionality included in winlogon.pl)
  * created new plugins
    * srun\_tln.pl, urun\_tln.pl,cmdproc\_tln.pl
    * -cmd\_shell\_tln.pl,muicache\_tln.pl

  * added alertMsg() functionality to rip.pl, rr.pl, and plugins
    * appcompatcache.pl, appcompatcache\_tln.pl
    * appinitdlls.pl
    * soft\_run.pl, user\_run.pl
    * imagefile.pl
    * winlogon.pl, winlogon\_u.pl
    * muicache.pl (look for values with "[Tt](Tt.md)emp" paths)
    * attachmgr.pl (look for values per KB 883260)
    * virut.pl
    * cmdproc.pl, cmd\_shell.pl

## 20130411 ##
  * retired specaccts.pl & notify.pl; incorporated functionality into winlogon.pl

## 20130410 ##
  * retired taskman.pl; merged into winlogon.pl
  * updated winlogon.pl (Wow6432Node support, etc.)
  * updated winlogon\_u.pl (Wow6432Node support)
  * updated shellexec.pl, imagefile.pl, installedcomp.pl (Wow6432Node support)

## 20130409 ##
  * added drivers32.pl (C. Harrell) to the archive

## 20130408 ##
  * updated bho.pl to support Wow6432Node

## 20130405 ##
  * updated cmd\_shell.pl to include Clients subkey in the Software hive
  * created cmd\_shell\_u.pl
  * fixed issue with rip.exe syntax info containing 'rr'
  * fixed banner in findexes.pl