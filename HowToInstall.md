

# TLDR (Too Long Didn't Read) #

  1. Use the installer from the downloads tab
  1. Start Autodesk Revit Architecture 2011

# Introduction #

RevitPythonShell is still a work-in-progress. I have only a first rough cut at an installer, so you are going to get your hands slightly dirty here.

Oh, you will definitely want to install IronPython first. (NOTE: add instructions here)

The installation breaks down to following steps:

  * either
    * run the [installer](http://revitpythonshell.googlecode.com/files/Setup_RevitPythonShell_1.0.msi)
    * build the `RevitPythonShell.dll`
  * register it as an external application in Autodesk Revit Architecture 2010
  * configure `RevitPythonShell.xml`
    * set up
    * add your own canned scripts

# Details #

## Build the `RevitPythonShell.dll` ##

  1. check out the source code (see http://code.google.com/p/revitpythonshell/source/checkout)
  1. open the solution in Visual Studio 2008 and build it
  1. remember the output directory of the build (something like 'projectlocation\bin\Debug'

## Register it as an external application in Autodesk Revit Architecture 2010 ##

add something like this to your `Revit.ini` file (see Revits developer documentation on how to do this):
```
[ExternalApplications]
EACount=1
EAName1=RevitPythonShell
EADescription1=
EAAssembly1=C:\Visual Studio 2008\Projects\revitpythonshell\RevitPythonShell\bin\Debug\RevitPythonShell.dll
EAClassName1=RevitPythonShell.RevitPythonShellApplication
```

## Configure the `RevitPythonShell.xml` ##

The `RevitPythonShell.xml` file contains some information read at startup time:

  * a list of search paths to be added to the interpreter
  * a list of canned commands (to be accessed via a button)
  * a default script to show in the input window

### Search Paths ###

The version of this file in source control adds two search paths by default:

  * `C:\Python25\Lib`
  * `C:\RevitPythonShell`

You will obviously want to set the path to the CPython library on your system for access to the standard library functions (quite handy...)

I use the folder `C:\RevitPythonShell` for all my own scripts, as it is easy to locate when I open these files in an editor etc.

### Canned Commands ###

The _name_ attribute will be displayed as a button text on top of the input window. Clicking on it will execute the command specified by the _src_ attribute.