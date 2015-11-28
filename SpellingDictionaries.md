# Obtaining dictionaries #

The TeXworks progam does not currently include any bundled spelling dictionaries. Therefore, if you want spell-checking to be enabled in the editor, you will need to install dictionaries separately.

The editor uses the [hunspell](http://hunspell.sourceforge.net/) spell-checker; more information is available at that project's site. Hunspell also supports dictionaries from the older myspell program.

One easy source of dictionaries is the OpenOffice.org project, which uses the same spelling engine. There is a list of available dictionaries at http://extensions.services.openoffice.org/. Note that TeXworks can only use the spelling dictionaries (`*.dic` and `*.aff`) for each language; to get them, rename the downloaded .oxt file to .zip and extract the spelling dictionary files (they may be contained in a subdirectory).

# Installing #

The dictionaries are installed in different locations depending on your platform.
_Note: The paths given below apply to the default configuration of the versions distributed here. If you use TeXworks as provided by a TeX distribution, the paths may differ._

## Windows ##

To find the correct folder, use "Help -> Settings and Resources...", navigate to the "Resources" folder given there, and finally put the spelling dictionaries in the `dictionaries` folder (if it doesn't exist, create it).

By default, the TeXworks resources directory should be located in your "user profile" directory, typically `C:\Documents and Settings\Your Name\`. This is automatically created the first time you run TeXworks, and some default resources are copied there. There should be a `dictionaries` subdirectory, but it is initially empty. Place the `*.dic` and `*.aff` files there, and then re-start TeXworks.

## Mac OS X ##

To find the correct folder, use "Help -> Settings and Resources...", navigate to the "Resources" folder given there, and finally put the spelling dictionaries in the `dictionaries` folder (if it doesn't exist, create it).

By default, the TeXworks resources folder should be located inside the Library folder of your Home (user) folder. This is automatically created the first time you run TeXworks, and some default resources are copied there. There should be a `dictionaries` subdirectory, but it is initially empty. Place the `*.dic` and `*.aff` files there, and then re-start TeXworks.

## GNU/Linux ##

On these systems, it is quite likely that appropriate dictionaries are already present, thanks to other programs using the same spell-check engine. However, if you need to add dictionaries, they should be placed in `/usr/share/myspell/dicts`. (This will typically require administrative privileges. I guess we'll offer some way to install "personal" dictionaries as a non-privileged user in the future.)

On some systems, the dictionaries are put elsewhere (for instance in `/usr/share/hunspell/`).
In this case, you can do:

    # cd /usr/share/myspell/dicts
    # ln -s /usr/share/hunspell/en_US.aff
    # ln -s /usr/share/hunspell/en_US.dic