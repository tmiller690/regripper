# Tools #
RegRipper is actually a suite of tools that all rely on a core set of functionality.


## Helper Functions ##
The main user interface (UI) tools for RegRipper (ie, the _RegRipper_ GUI and the _rip_ CLI tools) provide a number of functions to the plugins.  These functions are included in a separate **.pl file, and are accessed by the UI code via the _require_ pragma (allows the code to be loaded at run-time).  This allows for the following:**

  * The one set of code is available to the UI tools in a uniform manner.
  * The helper function code can updated and made available without requiring the tools themselves to be completely recompiled.
  * The code is completely transparent; anyone can open the helper files and see what the code is doing.

Note: In order to make the code portable and usable by the widest range of users, any modules required to use the helper functions (ie, _Time::Local_) will be compiled into the UI.