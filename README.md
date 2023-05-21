# IconFontCppHeaders for NeoDoa Game Engine

[https://github.com/juliettef/IconFontCppHeaders](https://github.com/juliettef/IconFontCppHeaders)

[https://github.com/NeoDoa-Collective/IconFontCppHeaders](https://github.com/NeoDoa-Collective/IconFontCppHeaders)

C, C++ headers for icon fonts Font Awesome.

A set of header files and classes for using icon fonts in C, C++, along with the python generator used to create the files.

Each header contains defines for one font, with each icon code point defined as ICON_*, along with the min, max and max 16 bit code points for font loading purposes. The min excludes the ASCII characters code points. The max 16 bit is for use with libraries that only support 16 bit code points, for example Dear ImGui.

In addition the python script can be used to convert ttf font files to C and C++ headers. 
Each ttf icon font file is converted to a C and C++ header file containing a single array of bytes. 
To enable conversion, run the GenerateIconFontCppHeadersOnly.py script with 'ttf2headerC = True'. 

## Icon Fonts

*Due to the nature of NeoDoa's requirements, support for most of the font sets are dropped.*

~~Font Awesome~~  
~~Font Awesome 4~~  
~~Font Awesome 5 free~~  
~~Font Awesome 5 pro~~

#### Font Awesome 6 free
* [github.com/FortAwesome/Font-Awesome/tree/6.x](https://github.com/FortAwesome/Font-Awesome/tree/6.x)
* [icons.yml](https://github.com/FortAwesome/Font-Awesome/blob/6.x/metadata/icons.yml)
* [fa-brands-400.ttf](https://github.com/FortAwesome/Font-Awesome/blob/6.x/webfonts/fa-brands-400.ttf)
* [fa-regular-400.ttf](https://github.com/FortAwesome/Font-Awesome/blob/6.x/webfonts/fa-regular-400.ttf)
* [fa-solid-900.ttf](https://github.com/FortAwesome/Font-Awesome/blob/6.x/webfonts/fa-solid-900.ttf)

#### Font Awesome 6 pro
* Commercial product, not supported but [generation should be similar to FA5 Pro](#notes-about-font-awesome-5-and-6), or see [@jakerieger's fork](https://github.com/jakerieger/IconFontCppHeaders)

~~Fork Awesome~~  
~~Google Material Design icons~~  
~~Kenney Game icons and expansion~~  
~~Fontaudio~~  
~~Codicons~~  
~~Ionicons and webfont Material Design Icons~~

### Notes about Font Awesome 5 and 6
#### Codepoints grouping
Font Awesome 5 and 6 split the different styles of icons into different font files with identical codepoints for *light*, *regular* and *solid* styles, and a different set of codepoints for *brands*. We have put the brands into a separate header file.
#### Generating Pro header files (Font Awesome 5)
Download the Font Awesome Pro Web package from [fontawesome.com](https://fontawesome.com). To generate the headers, drop *icons.yml* in the same directory as *GenerateIconFontCppHeaders.py* before running the script. The file *icons.yml* is under *..\fontawesome-pro-n.n.n-web\metadata\icons.yml* where *n.n.n* is the version number.

Icon files: 

* ..\fontawesome-pro-n.n.n-web\metadata\icons.yml  
* ..\fontawesome-pro-n.n.n-web\webfonts\fa-brands-400.ttf  
* ..\fontawesome-pro-n.n.n-web\webfonts\fa-light-300.ttf  
* ..\fontawesome-pro-n.n.n-web\webfonts\fa-regular-400.ttf  
* ..\fontawesome-pro-n.n.n-web\webfonts\fa-solid-900.ttf


## Example Code

Using [Dear ImGui](https://github.com/ocornut/imgui) as an example UI library:

```Cpp

#include "IconsFontAwesome5.h"

ImGuiIO& io = ImGui::GetIO();
io.Fonts->AddFontDefault();
float baseFontSize = 13.0f; // 13.0f is the size of the default font. Change to the font size you use.
float iconFontSize = baseFontSize * 2.0f / 3.0f; // FontAwesome fonts need to have their sizes reduced by 2.0f/3.0f in order to align correctly

// merge in icons from Font Awesome
static const ImWchar icons_ranges[] = { ICON_MIN_FA, ICON_MAX_16_FA, 0 };
ImFontConfig icons_config; 
icons_config.MergeMode = true; 
icons_config.PixelSnapH = true; 
icons_config.GlyphMinAdvanceX = iconFontSize;
io.Fonts->AddFontFromFileTTF( FONT_ICON_FILE_NAME_FAS, iconFontSize, &icons_config, icons_ranges );
// use FONT_ICON_FILE_NAME_FAR if you want regular instead of solid

// in an imgui window somewhere...
ImGui::Text( ICON_FA_PAINT_BRUSH "  Paint" ); // use string literal concatenation
// outputs a paint brush icon and 'Paint' as a string.
```

## Credits

Development - [Juliette Foucaut](http://www.enkisoftware.com/about.html#juliette) - [@juliettef](https://github.com/juliettef)  
Requirements - [Doug Binks](http://www.enkisoftware.com/about.html#doug) - [@dougbinks](https://github.com/dougbinks)  
None language implementation and [refactoring](https://gist.github.com/paniq/4a734e9d8e86a2373b5bc4ca719855ec) - [Leonard Ritter](http://www.leonard-ritter.com/) - [@paniq](https://github.com/paniq)  
Suggestion to add a define for the ttf file name - [Sean Barrett](https://nothings.org/) - [@nothings](https://github.com/nothings)  
Initial Font Awesome 5 implementation - [Codecat](https://codecat.nl/) - [@codecat](https://github.com/codecat)  
Suggestion to add Fork Awesome - [Julien Deswaef](http://xuv.be/) - [@xuv](https://github.com/xuv)  
Suggestion to add Ionicons - [Omar Cornut](http://www.miracleworld.net/) - [@ocornut](https://github.com/ocornut)  
C# language implementation - Rokas Kupstys - [@rokups](https://github.com/rokups)  
Suggestion to add Material Design Icons - Gustav Madeso - [@madeso](https://github.com/madeso)  
Fontaudio implementation - [Oli Larkin](https://www.olilarkin.co.uk/) - [@olilarkin](https://github.com/olilarkin)  
Initial ttf to C and C++ headers conversion implementation - Charles Mailly - [@Caerind](https://github.com/Caerind)  
Python language implementation - Hang Yu - [@yhyu13](https://github.com/yhyu13)  
Go language implementation - Matt Pharr - [@mpp](https://github.com/mmp)  
Codicons implementation - Robert Ryan - [@rtryan98](https://github.com/rtryan98)  
Rust language implementation - Gaeel Bradshaw-Rodriguez - [@Bradshaw](https://github.com/Bradshaw)  
Additional development for NeoDoa - [Doğa Oruç](aeris170.github.io) - [@aeris170](https://github.com/aeris170)