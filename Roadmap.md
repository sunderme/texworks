

This page documents the future goals for the TeXworks project. None of them are set in stone, however, and they are by no means exhaustive. If you have any other ideas, please open an issue here or put it up for discussion on the [mailing list](http://tug.org/mailman/listinfo/texworks).

There are no concrete dates given deliberately. The time it takes to complete the listed milestones may depend on many factors. TeXworks is a community project, however, so if you want to help getting things done faster (and know some C++), have a look at the [IdeasAndProjects](IdeasAndProjects.md) page on particular projects that need to get done.

## 0.6 series ##
The main target for this release is the PDF previewer.

Potential development targets include:
  * rewrite of the pdf previewer into a separate component
  * continuous scrolling & recto/verso display
  * support for high magnifications
  * additional tools (e.g., a measuring tool, a text select tool, ...)
  * improved presentation support (e.g., page transitions)

## 0.8 series ##
The main target for this release is the editor

Potential development targets include:
  * rewrite of the editor into a separate component
  * improved auto-completion and syntax highlighting
  * line folding
  * automatic encoding detection

## and beyond ##
Beyond the 0.8 series, there are a number of ideas that are not put into any timeline yet (and/or may rely on the successful completion of some of the milestones mentioned above):
  * improved scripting (e.g., enabling scripts to call other scripts or to respond to Qt signals for implementing, e.g. character palettes)
  * generic window handling (e.g., tabbed editing/previewing)
  * project management