
# Table of Contents

1.  [aRMSD &#x2013; minimalWindowsSupport](#org3cd8455)
    1.  [background](#orgb3f74f6)
    2.  [tools](#orgf469c2e)
    3.  [Install process](#org57c585c)
    4.  [Working with the fix](#org82c135f)
    5.  [Known limitations of this fix](#org1f34c0f)


<a id="org3cd8455"></a>

# aRMSD &#x2013; minimalWindowsSupport


<a id="orgb3f74f6"></a>

## background

`aRMSD` (<https://github.com/nbehrnd/aRMSD>), a program to compare
molecular structures with each other, works sufficiently well in an
ecosystem of Debian (reference system, testing / Sid toward
version 10 / Buster), or Xubuntu (test system was Xubuntu 18.04
LTS, point release 18.04.1) if the model data are provided in the
`*.xyz` format.  With the help of `openbabel` (version 2.4.1), it
equally reads *some* model data in the `*.pdb` format, too.

At present (December 2018), however, the instructions provided by
the original developer of the program, Arne Wagner, to render the
program functional in the Windows environment *appear* to be
invalidated by the continued development of the vtk-rendering
engine `aRMSD` relies.<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>

*This* project aims to provide *an elementary* support for `aRMSD`
in Windows, allowing to use the program *at all* &#x2013; even if some of
the functions of the program are unavailable.  It is meant as a *ad
hoc* and temporary fix only and assumes Windows 7 Pro (64 bit).  At
present, there is no similar fix addressing the 32 bit variant of
this platform.


<a id="orgf469c2e"></a>

## tools

The footprint of this *temporary fix* is quite large (about 2 GB
permanent hard disk space is needed), but is portable (e.g., USB
thumb-drive) since it does not affect the `PATH` variable of
Windows.  The fix works well-enough (*vide infra*) on a fresh
installation of Windows 7 Professional (64 bit).

On one hand, it relies on `WinPython` (version
`WinPython64-3.6.7.0Qt5`) mirrored from<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup> providing
Python 3.6.  Among this compilation, some of the dependencies
outlined by Arne Wagner are already included: `matplotlib`,
`uncertainties`, and performance related `cython`.  With 488 MB
size (as compressed archive), it is too large to be mirrored here,
but beside on the project page itself you find it here on
GitHub.<sup><a id="fnr.3" class="footref" href="#fn.3">3</a></sup>

The other *essential* dependency of `aRMSD` is the vtk-rendering
engine.<sup><a id="fnr.4" class="footref" href="#fn.4">4</a></sup> Currently, the wheel-directory maintained by
Christoph Gohlke<sup><a id="fnr.5" class="footref" href="#fn.5">5</a></sup> provides only one vtk-wheel
working smoothly with the versions of WinPython tested.  It is
worth about 27 MB and mirrored in *this* repository, too.

The two are characterized by these md5sums:

    2254b65e50a8c1834d10d253e243d23a  VTK-7.1.1-cp36-cp36m-win_amd64.whl
    72b0612de9fdc341e87f01d9ca7b230f  WinPython64-3.6.7.0Qt5.exe


<a id="org57c585c"></a>

## Install process

It is mandatory that the hosting Windows operating system is
64 bit.  Since the system's `PATH` variable is not touched, no
administrator privilege is required.  Anticipate about 2 GB disk
space to be used since `WinPython` will provide you with many more
packages than only the ones needed to run `aRMSD`.

Download the two files into a directory easy accessible for you.  A
mouse double-click on the `WinPython` executable will extract this
archive.  After about one or two minutes, the newly generated
folder `WPy-3670` equally contains an entry

    WinPython Control Panel.exe

which basically is the package manager of `WinPython`.  A
double-click on this opens this.  Choose now the index card
`Install / Upgrade Packages`.  In the bottom left corner of this
display, you find a button to point this manager to the location of
the vtk-wheel.  After a few moments, this selection will show up in
the main menu of the manager, too.  Subsequently, push the button
in the bottom right corner to add the wheel to the packages
considered by `WinPython` eventually managed within the `WPy-3670`
folder.  Again after a few moments (about 10 sec), the manager will
install the wheel.

Once the intermediate installation notifier clears up, you may close
the manager entirely.


<a id="org82c135f"></a>

## Working with the fix

Folder `WPy-3670` contains its own CLI, `WinPython Command
   Prompt.exe`.  A mouse double-click will open this.  As with the
native Windows `cmd.exe`, enter the directory of `aRMSD` housing
`aRMSD.py`.  You launch the program with

    python aRMSD.py


<a id="org1f34c0f"></a>

## Known limitations of this fix

Again, this solution is meant as *temporary fix* only.  Hence, not
requiring assistance by `openbabel`<sup><a id="fnr.6" class="footref" href="#fn.6">6</a></sup> to convert file
formats, `aRMSD` reads most likely *only* model data provided in
the `*.xyz` format.  However, alignment and scrutiny of these,
including report generation in a permanent log and provision of the
statistics plots are functional.  It actually *is expected* that
`aRMSD` will inform you about the missing link to `openbabel`.
(Since this fix does not accesses the `PATH` variable, it will not
recognize `openbabel` even if it were installed on the hosting
computer, either.)

If you need to compare models in a file format different than
`*.xyz`, the freeware `openabel` may assist in the data conversion
toward this format.

Equally, some of options accessible in the Linux-based use (e.g.,
anaglyph representation, less dominating display of the coordinate
system by vtk) are skipped here.


# Footnotes

<sup><a id="fn.1" href="#fnr.1">1</a></sup> Compare the issue deposit in the original branch of the
program, <https://github.com/armsd/aRMSD/issues>.

<sup><a id="fn.2" href="#fnr.2">2</a></sup> <https://winpython.github.io/>

<sup><a id="fn.3" href="#fnr.3">3</a></sup> Project site's entry:
<https://github.com/winpython/winpython/releases/tag/1.11.20181031>,
download link:
<https://github.com/winpython/winpython/releases/download/1.11.20181031/Winpython32-3.6.7.0Qt5.exe>

<sup><a id="fn.4" href="#fnr.4">4</a></sup> See <https://www.vtk.org/> and
<https://en.wikipedia.org/wiki/VTK>.

<sup><a id="fn.5" href="#fnr.5">5</a></sup> Unofficial Windows Binaries for Python Extension
Packages, <https://www.lfd.uci.edu/~gohlke/pythonlibs/>, accessed in
December 2018.

<sup><a id="fn.6" href="#fnr.6">6</a></sup> Open Babel: The Open Source Chemistry Toolbox, <http://openbabel.org/wiki/Main_Page>
