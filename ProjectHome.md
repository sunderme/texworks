### What is TeXworks? ###

An environment for authoring TeX (LaTeX, ConTeXt, etc) documents, with a Unicode-based, TeX-aware editor, integrated PDF viewer, and a clean, simple interface accessible to casual and non-technical users.

TeXworks is inspired by Dick Koch's award-winning [TeXShop](http://www.uoregon.edu/~koch/texshop/) program for Mac OS X, which has made quality typesetting through TeX accessible to a wider community of users, without a technical or intimidating face. The goal of TeXworks is to deliver a similarly integrated, easy-to-use environment for users on other platforms, especially GNU/Linux and Windows.

For more information, see the [TeXworks](http://tug.org/texworks/) page at the [TeX Users Group](http://tug.org/) site. There is also a [mailing list](http://tug.org/mailman/listinfo/texworks/) available for discussion of the project.

Alain Delmotte has written a manual for TeXworks, available at [his web site](http://www.leliseron.org/texworks/); the manual is also included as a Help file in the Windows and Mac binary distributions.

### Requirements ###

To build the current version of TeXworks from source, you will need to install developer packages (or equivalent) for:

  * Qt4 (4.5.2 is recommended, although the application may build with versions as old as 4.3.x. Note that on GNU/Linux, TeXworks may crash when changing the spell-checking language when using Qt 4.3.x. Updating to at least Qt 4.4.0 solves this.)
> http://qt.nokia.com/downloads

  * Poppler (using the latest stable release, currently 0.12, is strongly recommended, although versions as old as the 0.6 series should still work)
> http://poppler.freedesktop.org/

  * Hunspell (release 1.2.8 is recommended; earlier 1.2.x releases may be used, although support for some non-Latin-script languages may be lacking)
> http://hunspell.sourceforge.net/

  * libdbus (on X11-based platforms only; not used on Mac OS X or Windows)
> http://dbus.freedesktop.org/

along with their dependencies (such as Freetype, fontconfig, zlib, etc.) Details will depend on your platform. On GNU/Linux or similar systems, your package manager can probably provide all these. Feel free to contribute distribution-specific notes for the [Building](Building.md) page.

After installing the necessary libraries (and their headers), check the TeXworks.pro file and update paths as necessary; some of the paths currently in the project file are specific to one of my build machines.

Once the project file is correct, run `qmake` to create a Makefile or Xcode project, and then run `make` or use Xcode to build the application. Do not run `qmake -pro` to recreate the `.pro` file, as it has been hand-edited.

_Note:_ on some systems, the default `qmake` may be a Qt3 version, in which case it will generate lots of warnings, and `make` will fail miserably; TeXworks is a Qt4 program. In that case, see if you have `qmake-qt4`, or perhaps run the Qt4 version using a full path.

The current version of TeXworks has been successfully built with

  * Xcode (using gcc 4) on Mac OS X (built on 10.5, but should run on 10.4 or later)
  * MinGW release 5.1.4 on Windows XP (also runs on Vista and Windows 7)
  * gcc 4 on GNU/Linux, various BSDs, etc.

Getting all the right libraries built and installed for the mingw32 build can be tricky. By slightly patching poppler 0.12, it is possible to build a version that does not depend on fontconfig (and thence on various other libraries). See the `poppler-patches` directory in the source repository.

To avoid having to build poppler and its dependencies for Windows, you can get precompiled libraries from the KDE on Windows project.

Further tips on building TeXworks from source are available on some of the wiki pages.