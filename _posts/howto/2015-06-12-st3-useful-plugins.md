---
layout: post
title: Sublime Text 3 - Useful Plugins
category: How-To
tags: sublimetext3 tips program how-to
description: tips know how series
---

By [Ferdian Pratama](http:/ferdianap.github.io/)

Latest update: Jun 12, 2015 13:50:17 PM

<!-- MarkdownTOC depth=3 -->

- C++ syntax specific settings
- Installed packages
	- Package Control
	- Word Count
	- LaTeX WordCount
	- Color Sublime
	- Theme - Spacegray
	- Theme - Asphalt
	- Markdown TOC
	- Diffy
	- LaTeX Tools
	- InsertDate
	- Markdown Editing
	- Markdown Preview
	- OmniMarkupPreviewer
	- SidebarFolders
	- Alignment
	- Sidebar Enhancement
	- Anaconda
	- ExportHTML
	- Run Matlab script
	- Build and run cpp code
	- ASTYLE FORMATTER
	- SUBLIME REPL
	- Installing OpenCV in Windows and ST3
	- Install Boost library on Windows 8
	- Docblockr
	- Git & GitGutter

<!-- /MarkdownTOC -->

## C++ syntax specific settings

Add the following code in the settings

```yaml
{
    "word_wrap": true,
    "wrap_width": 78
}
```

## Installed packages

To see more features of ST3, check out [https://scotch.io/bar-talk/best-of-sublime-text-3-features-plugins-and-settings]()

### Package Control

See [https://packagecontrol.io/installation]()

### Word Count

See [https://github.com/titoBouzout/WordCount]()

### LaTeX WordCount

See [https://github.com/lionandoil/SublimeLaTeXWordCount]()

The default key binding is <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>C</kbd>

### Color Sublime

See [https://github.com/Colorsublime/Colorsublime-Plugin]()

Download the themes from [http://colorsublime.com/]()
and go to `Preference > Browse Package ...`
copy all the `.tmTheme` files into a folder named *Colorsublime-Themes*

### Theme - Spacegray

See [https://github.com/kkga/spacegray]()

Go to `Preference > Settings - User`, copy and paste the following

```yaml
{
	"color_scheme": "Packages/Colorsublime-Themes/FireCode.tmTheme",
	"ignored_packages":
	[
		"Vintage"
	],
	"theme": "Spacegray.sublime-theme"
}

```

### Theme - Asphalt

See [https://github.com/Orlmente/Theme-Asphalt]()

```yaml
{
    "theme": "Asphalt.sublime-theme"

    // Alternatives
    // Asphalt-monochrome
    // Asphalt-green
    // Asphalt-blue
    // Asphalt-orange
}
```

To get more themes, see [https://scotch.io/bar-talk/the-best-sublime-text-3-themes-of-2014]()

### Markdown TOC

See [https://github.com/naokazuterada/MarkdownTOC]()

#### Feature

- Insert Table of Contents depending on headings in document
- TOC reflects contents from below its position or cursor (when you select `Insert TOC` menu)
- Auto linking when heading has anchor
- Refresh contents when file is saving
- [Control TOC depth in its comment tags][depth-control]

#### Using

1. Open Markdown files.
2. Move cursor to position where you want to `insert TOC`.
3. `Tools > MarkdownTOC > Insert TOC`
4. TOC has inserted into document!
5. Update contents and save...
6. TOC has been updated.

***Don't remove the comment tags if you want to update every time saving.***


#### Depth control [depth-control]

You can control TOC depth in its comment tags.

```xml
<!-- MarkdownTOC depth=2 -->

- foo
- bar
- buz
- qux

<!-- /MarkdownTOC -->
```

```xml
<!-- MarkdownTOC depth=3 -->

- foo
- bar
  - qux
  - quux
- buz
- qux

<!-- /MarkdownTOC -->
```

You can also set default depth in Settings.

`Preference > Package Settings > MarkdownTOC > Settings - User`

```yaml
{
"default_depth": 0
}
```

`depth=0` means no limit


### Diffy

See [https://github.com/zsong/diffy]()

After install the plugin, set the layout to be 2 columns via View -> Layout -> Columns: 2. And make sure you have files (or temporary files pasted from clipboard) opened side by side.

To compare and show the diffs, press <kbd>Ctrl</kbd>+<kbd>K</kbd> followed by <kbd>Ctrl</kbd>+<kbd>D</kbd>.

To clear the marked lines, press press <kbd>Ctrl</kbd>+<kbd>K</kbd> followed by <kbd>Ctrl</kbd>+<kbd>C</kbd>.

### LaTeX Tools

See [https://github.com/SublimeText/LaTeXTools]()

1. Install MikTex for Windows, or TexLive for Windows, Mac and Linux.
2. For first time install, open the command palette from the Tools menu, search for "LaTeXTools: Reconfigure and migrate settings.
3. Install Sumatra PDF for Windows (the latest version)
4. Add sumatra pdf to the PATH (Environment variable) to `C:\Program Files (x86)\SumatraPDF` if it is in default install dir, or to `F:\Win8App\SUMATRAPDF`
5. Open a manuscript PDF that has a sync info related to '.synctex.gz' file, and look for the inverse-search command line at the bottom of the options dialog, and replace it with `"F:\Win8App\ST3\sublime_text.exe" "%f:%l"` with the directory of the sublime_text.exe file.
6. Edit the `LaTeX.sublime-settings` in the `User` directory to make sure that the configuration reflects your preferred TeX distribution. Open the file and scroll down to the section titled "Platform settings." Look at the block for your OS, namely windows. Within that block, verify that the texpath setting is correct; for MiKTeX, you can leave this empty, i.e., "". If you do specify a path, note that it must include the system path variable, i.e., $PATH (this syntax seems to be OK). Also verify that the distro setting is correct: the possible values are "miktex" and "texlive". i.e.: `"texpath" : "C:\\texlive\\2014\\bin\\win32;$PATH",`
7. Change the `builder` into `simple`.

To Compile: <kbd>Ctrl</kbd>+<kbd>B</kbd>

To Fwd Search: <kbd>Ctrl</kbd>+<kbd>L</kbd>, <kbd>J</kbd>

To Inv Search: double click in the PDF


### InsertDate

See [https://github.com/FichteFoll/sublimetext-insertdate]()

Preference > Package Settings > InsertDate > Settings - User
then copy the following and save.

```json
{
	"keys": ["ctrl+f5", "ctrl+f5"],
    "command": "insert_date",
    "format": "%b %d, %Y %H:%M:%S %p"
}
```

To launch the menu, press <kbd>F5</kbd> .
To directly insert the default timestamp, press <kbd>Ctrl</kbd>+<kbd>F5</kbd> twice.

To make a custom format, visit [http://www.strfti.me/]()

### Markdown Editing

See [https://github.com/SublimeText-Markdown/MarkdownEditing]()

In order to activate the dark or the yellow theme, put one of these lines to your user settings file of the flavor (Packages/User/[flavor].sublime-settings):

```json
"color_scheme": "Packages/MarkdownEditing/MarkdownEditor-Dark.tmTheme",
"color_scheme": "Packages/MarkdownEditing/MarkdownEditor-Yellow.tmTheme",
```

Restart after installation finished, and change the extension into Markdown GFM.

### Markdown Preview

#### To preview :

- optionally select some of your markdown for conversion
- use <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> then `Markdown Preview` to show the follow commands (you will be prompted to select which parser you prefer):
- Markdown Preview: Preview in Browser
- Markdown Preview: Export HTML in Sublime Text
- Markdown Preview: Copy to Clipboard
- Markdown Preview: Open Markdown Cheat sheet
- or bind some key in your user key binding, using a line like this one:
 `{ "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} },` for a specific parser and target or `{ "keys": ["alt+m"], "command": "markdown_preview_select", "args": {"target": "browser"} },` to bring up the quick panel to select enabled parsers for a given target.
- once converted a first time, the output HTML will be updated on each file save (with LiveReload plugin)

#### To build :

- Just use <kbd>Ctrl</kbd>+<kbd>B</kbd> (Windows/Linux) or <kbd>Cmd</kbd>+<kbd>B</kbd> (Mac) to build current file.

#### To config :

Using Sublime Text menu: `Preferences`>`Package Settings`>`Markdown Preview`

- `Settings - User` is where you change your settings for Markdown Preview.
- `Settings - Default` is a good reference with detailed descriptions for each setting.


### OmniMarkupPreviewer

See [https://github.com/timonwong/OmniMarkupPreviewer]()

To preview, just <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>O</kbd> and it will update automatically without manual refresh browser.

**Note:** this is only standard markdown, not GFM!

### SidebarFolders

See [https://github.com/titoBouzout/SideBarFolders]()

This allows quick switch of the opened folders without within the same window.
Notice the Folder ToolBar.

### Alignment

See [http://wbond.net/sublime_packages/alignment]()

Highlight the lines and <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>A</kbd>.

### Sidebar Enhancement

See [https://github.com/titoBouzout/SideBarEnhancements]()

### Anaconda

After Anaconda is installed, copy the following to `Anaconda.sublime-settings` for accessing its features.

```
{
    "python_interpreter": "C:\\Python27\\python.exe"
}
```

OPTIONAL: (FOR EXECUTION IN CMD)
After install python for windows, copy the following code and save as a file in the directory of `Packages/User/Python_cmd.sublime-build` in the browse package for building the file.

```
{
    "cmd": ["start", "cmd", "/k", "c:/python27/python.exe", "$file"],
    "selector": "source.python",
    "shell": true,
    "working_dir": "$file_dir"
}
```



### ExportHTML

install and export from <kbd>Ctrl</kbd>+<kbd>P</kbd> and find the options to export. Make sure that the default app for HTML is the browser for automatic printing option.

### Run Matlab script

```
{
  "cmd": ["C:\\Program Files\\MATLAB\\MATLAB Production Server\\R2015a\\bin\\matlab", "-nosplash", "-nodesktop",  "-r", "run('$file_name')"],
    "selector": "source.m"
}
```
navigate to `Tools > Build System > New Build System`, copy the above code into that file, and save the file as `matlab.sublime-build` in the directory Sublime recommends saving it to. Now, when you build a `.m` file in ST2, a lite version of MATLAB will open up and run your code. woo!
Also, to get Sublime Text 2 to nicely recognize `.m` files as MATLAB files, go to `View > Syntax > Open all with current extension as....` and select `MATLAB`.

### Build and run cpp code

install mingw version > 4.8.1 (tested ver. 4.9.2), download here
`http://sourceforge.net/projects/mingw-w64/files/latest/download?source=files`
and put the environment variable in path, like the following:
`C:\Program Files\mingw-w64\x86_64-4.9.2-posix-seh-rt_v4-rev2\mingw64\bin`.
4.9.2 x86_64 posix seh 3 -> in lenovo but rev 2 in lab

<kbd>Ctrl</kbd>+<kbd>B</kbd> to compile

<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>B</kbd> to run the code.

Optional: put the following in `cpp.sublime-build` in browse `package\user` if the built in doesnt work out of the box.

```
{
    "cmd": ["g++", "*.cpp", "-o", "${file_path}/${file_base_name}"],
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "working_dir": "${file_path}",
    "selector": "source.c, source.c++",

    "variants":
    [
        {
            "name": "Run",
            "cmd": ["${file_path}/${file_base_name}.exe"]
        }
    ]
}
```


### ASTYLE FORMATTER

Windows, Linux:

<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>F</kbd>: Format current file.

<kbd>Ctrl</kbd>+<kbd>K</kbd>, <kbd>Ctrl</kbd>+<kbd>F</kbd>: Format current selection.

OSX:

<kbd>Cmd</kbd>+<kbd>Alt</kbd>+<kbd>F</kbd>: Format current file.

<kbd>Cmd</kbd>+<kbd>K</kbd>, <kbd>Cmd</kbd>+<kbd>F</kbd>: Format current selection.

### SUBLIME REPL

see here: [https://github.com/wuub/SublimeREPL]()

### Installing OpenCV in Windows and ST3

1. install MinGW in as in the previous step and add to system path
2. Install OpenCV from [http://opencv.org/downloads.html]() or [http://sourceforge.net/projects/opencvlibrary/files/opencv-win/]() recommended ver 2.4.11 and extract to `C:\` (`F:\` for Lenovo)
3. Download and install CMAKE from [http://www.cmake.org/cmake/resources/software.html]()
4. Open cmake and select `C:\opencv\sources` as the source directory and `C:\opencv\build\x86\mingw` as the directory to build the binaries (you could select any directory but choosing this one will overwrite the pre-built OpenCV binaries and then the rest of the tutorial is the same. Click `configure` choose `minGW makefiles` wait and then click `generate`. When cmake is done we need to open a command prompt in the build directory, so navigate to `C:\opencv\build\x86\mingw` then shift right click and choose open command window here then type `mingw32-make`. Mingw will now start compiling OpenCV, this will take a bit so feel free to do something else, when you come back type `mingw32-make install`.
5. Add OpenCV to the system path `C:\opencv\build\x86\mingw\bin;C:\opencv\build\include` by navigating to `Control Panel > System > Advanced System Settings`
6. In the `cpp.sublime-build`, modify as needed below, and opencv can be used as usual.

The following is `cpp.sublime-build` for integration with opencv for WINDOWS

```
{
"cmd": ["g++", "-Wall",  "*.cpp", "-o", "${file_path}/${file_base_name}",
"-IC:\\opencv\\build\\include\\opencv2",
"-IC:\\opencv\\build\\include",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_calib3d2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_contrib2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_core2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_features2d2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_flann2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_gpu2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_highgui2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_imgproc2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_legacy2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_ml2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_nonfree2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_objdetect2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_ocl2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_photo2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_stitching2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_superres2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_ts2411.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_video2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_videostab2411.dll.a"],
"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
"working_dir": "${file_path}",
"selector": "source.c, source.c++",
 
"variants":
[{
    "name": "Run",
    "cmd": ["${file_path}/${file_base_name}.exe"]
}]
}
```


The following is `cpp.sublime-build` for integration with opencv for MAC.
My OpenCV was installed using HomeBrew, which has pkg-config information for opencv already created inside `/usr/Local/Cellar/opencv/2.4.4/lib/pkgconfig/`, thus you can utilize pkg-config to generate the include and library flags for g++ from it.

```
{
 "cmd": ["g++", "-Wall", "-Wextra", "${file}", "-o", "${file_path}/${file_base_name}",
 "-I/usr/local/Cellar/opencv/2.4.4/include/opencv",
 "-I/usr/local/Cellar/opencv/2.4.4/include",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_calib3d.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_contrib.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_core.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_features2d.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_flann.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_gpu.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_highgui.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_imgproc.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_legacy.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_ml.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_nonfree.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_objdetect.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_ocl.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_photo.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_stitching.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_ts.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_video.dylib",
 "/usr/local/Cellar/opencv/2.4.4/lib/libopencv_videostab.dylib"],
 "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
 "working_dir": "${file_path}",
 "selector": "source.c, source.c++",
 
"variants":
 [{
"name": "Run",
"cmd": ["bash", "-c", "g++ '${file}' -o '${file_path}/${file_base_name}' `/usr/bin/pkg-config --cflags --libs   /usr/Local/Cellar/opencv/2.4.4/lib/pkgconfig/opencv.pc` && '${file_path}/${file_base_name}' "]
}]
}
```

### Install Boost library on Windows 8

Source: 
[http://andres.jaimes.net/718/how-to-install-the-c-boost-libraries-on-windows/]()

Download and unzip the boost source code from [http://www.boost.org/](). I will unzip it to `C:\optc-libs`, but you can use the one you prefer. After you unzip, open a command line and go to your selected folder:

```
cd C:\optc-libs\boost_1_58_0
```

Start bootstrap.bat and specify your toolset. Toolsets supported by this script are: borland, como, gcc, gcc-nocygwin, intel-win32, metrowerks, mingw, msvc, vc7, vc8, vc9, vc10, vc11. In my case I will use the mingw toolset:

```
bootstrap.bat mingw
```

All required files for compilation should be ready. Now you have to define a installation directory and specify a toolset. Toolsets here are a little bit different from the ones we used before:

acc: Hewlett Packard, Only very recent versions are known to work well with Boost
borland: borland
como: Comeau Computing, Using this toolset may require configuring another toolset to act as its backend
darwin: Apple, Apple’s version of the GCC toolchain with support for Darwin and MacOS X features such as frameworks.
gcc: The Gnu Project, including Cygwin and MinGW
hp_cxx: Hewlett Packard, Targeted at the Tru64 operating system.
intel: Intel
msvc: Microsoft
sun: Sun, Only very recent versions are known to work well with Boost.
vacpp: IBM, The VisualAge C++ compiler.
Since I’m using MinGW I will use gcc.

`b2 install --prefix=c:/installation/path toolset=gcc`

In this case
`b2 install --prefix=F:\optc-libs toolset=gcc`


At this time you can go get a cup of coffee. Or maybe two.

When compilation ends, go to your selected installation path (watch out!, this is not the folder where you originally unzipped the source code). You will find two folders: include and lib. Both folders should contain files. That means you are done and ready for the testing phase.

If any of the afore mentioned folders is empty then we have problems. Common problems arise due to selecting the wrong toolset for compiling, so if your lib folder is empty try choosing a different toolset. If error persist, take a look at the compilation output. Errors must be shown there, specially at the last lines of the output.


***TESTING***

From your IDE create a file named main.cpp and copy the following text onto it:

```c++
#include <boost/regex.hpp>
#include 
#include 

int main()
{
    std::string line;
    boost::regex pat( "^Subject: (Re: |Aw: )*(.*)" );

    while (std::cin)
    {
        std::getline(std::cin, line);
        boost::smatch matches;
        if (boost::regex_match(line, matches, pat))
            std::cout << matches[2] << std::endl;
    }
}
```


***It's time to compile (and link)***

In order to let your compiler know where to look for the headers and libraries, you have to follow the next steps. You can usually accomplish them by right clicking on your project and selecting Properties or Options.

Add the following path to your includes list:
`C:/installation/path/include/boost-version`

Add the following path to your additional library directories list
`C:/installation/path/lib`
 
Important: if you are using Netbeans, you should only type /installation/path/lib (you have to omit the C:). For a very strange reason, Netbeans adds a forward slash at the beggining of the parameter /L used to compile (only when it begins with C:) resulting in an unknown path. This might be fixed in later versions.

If you are using a gnu compiler (that is Cygwin or MinGW), you must also add the specific library to the linker. If you are using Microsoft Visual Studio you can skip this step because it includes the so called auto-linking support. But, in my case, I have to add the following library to my libraries list so the linker performs without complaints:

`C:/installation/path/lib/libboost_regex-mgw47-mt-1_51.a`

This file name is composed by:
The standard lib prefix. DLL’s do not use it.
The library name boost_regex.
The toolset used to compile it, in my case mgw47, that is MinGW version 4.7.
The threading tag mt, which indicates if the library accepts multithreading.
The ABI tag, that can be: d for debugging, s for static linkage or g, y, p which are not covered in this text.
The version tag.
The extension, which can be `.lib` or `.a`.
 
You are ready. Build the program.

***Time to execute it***

The program you just compiled (and linked) can parse a text file looking for a line starting with the text “Subject:” in it. So to test it, copy and paste the following text into an empty text file and name it test.txt (save it in the folder where your `.exe` file resides):

```
To: George Shmidlap
From: Rita Marlowe
Subject: Will Success Spoil Rock Hunter?
---
See subject.
```

Now, from a command prompt type:

`yourprogram.exe < test.txt`

If everything goes right you should see the following text:

`Will Success Spoil Rock Hunter?`

The final c++.sublime-build integrated with boost:
```
{
"cmd": ["g++", "-Wall",  "*.cpp", "-o", "${file_path}/${file_base_name}",
"-IC:\\opencv\\build\\include\\opencv2",
"-IC:\\opencv\\build\\include",
"-IC:\\optc-libs\\include\\boost-1_58",
"C:\\optc-libs\\lib\\libboost_random-mgw49-mt-1_58.a",
"C:\\optc-libs\\lib\\libboost_regex-mgw49-mt-1_58.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_calib3d2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_contrib2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_core2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_features2d2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_flann2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_gpu2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_highgui2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_imgproc2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_legacy2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_ml2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_nonfree2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_objdetect2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_ocl2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_photo2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_stitching2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_superres2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_ts2411.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_video2411.dll.a",
"C:\\opencv\\build\\x86\\mingw\\lib\\libopencv_videostab2411.dll.a"],
"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
"working_dir": "${file_path}",
"selector": "source.c, source.c++",
 
"variants":
[{
    "name": "Run",
    "cmd": ["${file_path}/${file_base_name}.exe"]
}]
}
```


### Docblockr

[https://github.com/spadgos/sublime-jsdocs]()

### Git & GitGutter

For git integration