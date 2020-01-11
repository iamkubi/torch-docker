Building on the work of radu706 of the Torch Discord on getting the CLI version of Torch running under Wine, this Docker image brings the GUI version of Torch to the web and VNC so you can have a truly headless server.

In order to keep the image size down and simplify updates, this image contains *only* the Torch server and will download the Space Engineers dedicated server on first run. The SteamCMD update progress does not appear in the console but it *is* working.

**Warning:** This image is experimental and initial testing shows performance to be a fraction of running under Windows. Don't use it for production use.

Ports
-----
* TCP 5900: VNC (x11vnc)
* TCP 6080: Web UI (noVNC)
* UDP 27016: Game server

Known Bugs
----------
* Torch themes don't work
* Keen's remote API doesn't work
* Title bar doesn't work unless virtual desktop setting is run after first boot

Build Notes
-----------
* Space Engineers is *theoretically* okay with .NET Framework 4.0 and Visual C++ 2017 redistributables since that's what it ships with
* Torch is built against (according to `packages.config`) .NET Framework 4.6.1 and Visual C++ 2013
* However, booting with .NET Framework 4.6.1 on Wine results in fatal errors because of missing calls in a DLL, so you really need .NET Framework 4.6.2
* Booting with .NET Framework 4.7 or higher results in rendering issues
* Torch GUI requires Arial font to be installed or it'll fail fatally
* Window management must be disabled for Wine to render a titlebar and a virtual desktop must then be used to stop the cursor disappearing on window focus
* Winetricks setting verbs must be called individually or they only *appear* to work