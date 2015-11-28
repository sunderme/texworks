

# Introduction #

TeXworks comes with a variety of typesetting engines preconfigured. Among them are pdfLaTeX, ConTeXt (MKII), and XeLaTeX. In addition, some other tools such as BibTeX and MakeIndex are included.

Some other workflows are not preconfigured, however. Most notably, the tools for producing .dvi or .ps files are not predefined. This page summarizes ways to set up these tools.

Note that the procedures here are intended for expert users who know what they are doing. If you have no clue what this page is talking about and what different `*`TeX tools and output formats are out there, you're probably fine with the preconfigured engines.

# Defining new typesetting tools #
The typesetting tools can be edit via the "Preferences" dialog. To open it, click on "Preferences..." in the "Edit" menu. Then, click on the "Typesetting" tab at the top. The tools list (and the corresponding buttons) is located in the bottom. To add new tools, click on the button labeled "+". To remove a tool, select it and click on the button labeled "-". To edit a tool, select it and click on the "Edit..." button.

In the "Tool Configuration" dialog, you can specify a name, a program, and a list of arguments. In the list of arguments, you can use the following variables that get expanded just before the tool is started:
| $synctexoption | expands to "-synctex=1" if your tools support SyncTeX |
|:---------------|:------------------------------------------------------|
| $fullname | expands to the full name of your root document (e.g. rootfile.tex) |
| $basename | expands to the name (without extension) of your root document (e.g. rootfile) |
| $suffix | expands to the extension of your root document (e.g. tex) |
| $directory | expands to the absolute path to the directory containing your root document |

# Common Workflows #
## latexmk ##
Latexmk (http://www.phys.psu.edu/~collins/software/latexmk-jcc/) is a versatile typesetting tool that can do the whole typesetting for you. This includes running additional tools (such as BibTeX or MakeIndex) as well as running `*`TeX sufficiently often to resolve all references. It also includes support for additional output formats (.ps, .dvi) and additional workflows (ps2pdf, dvipdf) mentioned below.

In order to use latexmk, you must have it installed and set up (please refer to your TeX distribution for this). You can check if it works correctly by running `latexmk -v` from the command line (make sure you are in the directory containing latexmk before running the command). This should print the program's version.

To set up TeXworks to use latexmk for pdf output, create a new typesetting tool using the configuration
```
Program:   latexmk
Arguments: -e
           $pdflatex=q/pdflatex $synctexoption %O %S/
           -pdf
           $fullname

[X] View PDF after running
```

For other options, please refer to the manual coming with latexmk. Most notable are the switches "-dvi", "-ps", and "-pdfps". Note that in all those cases, you must replace all occurences of "pdflatex" in the arguments by "latex".

## simpdftex ##
simpdftex is a script for Linux/Mac that greatly simplifies the processes {la}tex -> dvips -> ps2pdf and {la}tex -> dvipdfm.

In order to use simpdftex, you must have it installed (please refer to your TeX distribution for this). You can check if it is available on your system by running `simpdftex` from the command line, which should print some information about the program.

To set up TeXworks to use simpdftex, create a new typesetting tool using the configuration
```
Program:   simpdftex
Arguments: latex
           --extratexopts
           $synctexoption
           $fullname

[X] View PDF after running
```
Replace "latex" by "tex" if you write plain TeX files. This executes the process latex -> dvips -> ps2pdf by default. For other options (e.g. for using an alternative to the ps2pdf distiller), please refer to the documentation fo simpdftex.

_Thanks to Bruno Voisin for pointing out this script_

## tex -> dvips -> ps2pdf ##
This is usually required if you want to use !PSTricks. Consider using PGF/TikZ instead.

_On Linux/Mac, please consider using simpdftex as described above._

Configuring this workflow is not straight-forward. TeXworks only supports running a single command at once, but you need to call "tex", "dvips", and ps2pdf. To be able to do that, you need to create a simple script, the content of which is platform dependent (see below). Then define a new typesetting tool using the following configuration:
```
Program:   <path to your script goes here>
Arguments: $basename

[X] View PDF after running
```

#### Windows ####
Create a file "tex-dvips-ps2pdf.bat" containing
```
@tex -synctex=1 "%1.tex" && dvips "%1.dvi" && ps2pdf "%1.ps"
```

If "-synctex=1" causes problems, simply remove it.

(see also http://tug.org/pipermail/texworks/2009q2/000822.html and http://tug.org/pipermail/texworks/2009q4/001903.html)

_Thanks to Tomek and Đức Minh Thái for providing this script_

#### Linux/Mac ####
Create a file "tex-dvips-ps2pdf.sh" containing
```
#!/bin/sh

tex -synctex=1 "$1.tex" && dvips "$1.dvi" && "$1.ps"
```
and make it executable (e.g. by running `chmod +x tex-dvips-ps2pdf.sh` from a terminal window).

If "-synctex=1" causes problems, simply remove it.

## latex -> dvips -> ps2pdf ##
This is usually required if you want to use !PSTricks. Consider using PGF/TikZ instead.

_On Linux/Mac, please consider using simpdftex as described above._

Configuring this workflow is not straight-forward. TeXworks only supports running a single command at once, but you need to call "latex", "dvips", and ps2pdf. To be able to do that, you need to create a simple script, the content of which is platform dependent (see below). Then define a new typesetting tool using the following configuration:
```
Program:   <path to your script goes here>
Arguments: $basename

[X] View PDF after running
```

#### Windows ####
Create a file "latex-dvips-ps2pdf.bat" containing
```
@latex -synctex=1 "%1.tex" && dvips "%1.dvi" && ps2pdf "%1.ps"
```

If "-synctex=1" causes problems, simply remove it.

(see also http://tug.org/pipermail/texworks/2009q2/000822.html and http://tug.org/pipermail/texworks/2009q4/001903.html)

_Thanks to Tomek and Đức Minh Thái for providing this script_

#### Linux/Mac ####
Create a file "latex-dvips-ps2pdf.sh" containing
```
#!/bin/sh

latex -synctex=1 "$1.tex" && dvips "$1.dvi" && ps2pdf "$1.ps"
```
and make it executable (e.g. by running `chmod +x latex-dvips-ps2pdf.sh` from a terminal window).

If "-synctex=1" causes problems, simply remove it.



# Common Output Formats #
## DVI ##
### TeX ###
Use the following configuration:
```
Program:   tex
Arguments: $synctexoption
           $fullname

[ ] View PDF after running
```

### LaTeX ###
Use the same configuration as for TeX, but use the program "latex" instead.

### ConTeXt (MKII) ###
Use the following configuration:
```
Program:   texmfstart
Arguments: texexec
           --dvi
           --nobackend
           $fullname

[ ] View PDF after running
```

## PS ##
### TeX ###
Configuring TeX for .ps output is not straight-forward. TeXworks only supports running a single command at once, but for producing .ps files one needs to call both "tex" and "dvips". To be able to do that, you need to create a simple script, the content of which is platform dependent (see below). Then define a new typesetting tool using the following configuration:
```
Program:   <path to your script goes here>
Arguments: $basename

[ ] View PDF after running
```

#### Windows ####
Create a file "tex-dvips.bat" containing
```
@tex "%1.tex" && dvips "%1.dvi"
```

(see also http://tug.org/pipermail/texworks/2009q2/000822.html and http://tug.org/pipermail/texworks/2009q4/001903.html)

_Thanks to Tomek and Đức Minh Thái for providing this script_

#### Linux/Mac ####
Create a file "tex-dvips.sh" containing
```
#!/bin/sh

tex "$1.tex" && dvips "$1.dvi"
```
and make it executable (e.g. by running `chmod +x tex-dvips.sh` from a terminal window).

### LaTeX ###
Configuring LaTeX for .ps output is not straight-forward. TeXworks only supports running a single command at once, but for producing .ps files one needs to call both "latex" and "dvips". To be able to do that, you need to create a simple script, the content of which is platform dependent (see below). Then define a new typesetting tool using the following configuration:
```
Program:   <path to your script goes here>
Arguments: $basename

[ ] View PDF after running
```

#### Windows ####
Create a file "latex-dvips.bat" containing
```
@latex "%1.tex" && dvips "%1.dvi"
```

(see also http://tug.org/pipermail/texworks/2009q2/000822.html and http://tug.org/pipermail/texworks/2009q4/001903.html)

_Thanks to Tomek and Đức Minh Thái for providing this script_

#### Linux/Mac ####
Create a file "latex-dvips.sh" containing
```
#!/bin/sh

latex "$1.tex" && dvips "$1.dvi"
```
and make it executable (e.g. by running `chmod +x latex-dvips.sh` from a terminal window).

### ConTeXt (MKII) ###
Use the following configuration:
```
Program:   texmfstart
Arguments: texexec
           --ps
           $fullname

[ ] View PDF after running
```

# Other tools #

## MetaPost ##
MetaPost can be used to create vector graphics based on plain text source files. One such source file can contain several drawings which MetaPost puts in specially named files. In order to preview them in TeXworks, you need to create a simple script, the content of which is platform dependent (see below). Running that script requires the open-source [pdftk](http://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/) program.

Once you have created the script, define a new typesetting tool using the following configuration:
```
Program:   <path to your script goes here>
Arguments: $basename
           $suffix

[X] View PDF after running
```

#### Windows ####
Create a file "MetaPost4TeXworks.bat" containing
```
@mptopdf "%1.%2" && pdftk "%1"-*.pdf output "%1.pdf"
```

#### Linux/Mac ####
Create a file "MetaPost4TeXworks.sh" containing
```
#!/bin/sh

mptopdf "$1.$2" && pdftk "$1"-*.pdf output "$1.pdf"
```
and make it executable (e.g. by running `chmod +x MetaPost4TeXworks.sh` from a terminal window).