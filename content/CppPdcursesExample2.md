



 

 

 

 

 

([C++](Cpp.htm)) [PdcursesExample2](CppPdcursesExample2.htm)
============================================================

 

![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Windows](PicWindows.png)

 

[PDCurses example 2: first modification](CppPdcursesExample2.htm) is a
[PDCurses](CppPdcurses.htm) example that is a modification of a tutorial
its code.

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.htm)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.htm) 15.04 (vivid)

[IDE(s)](CppIde.htm):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.htm) 3.1.1

[Project type](CppQtProjectType.htm):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.htm)

[C++ standard](CppStandard.htm):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.9.2

[Libraries](CppLibrary.htm) used:

-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppPdcursesExample2/CppPdcursesExample2.pro
--------------------------------------------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  include(../../Libraries/Pdcurses.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #       ../../Libraries/pdc25_vc_w32 # #   HEADERS += \ #       ../../Libraries/pdc25_vc_w32/panel.h \ #       ../../Libraries/pdc25_vc_w32/curses.h # #   LIBS += -L../../Libraries/pdc25_vc_w32 -lpdcurses # }  SOURCES += main.cpp`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppPdcursesExample2/main.cpp
------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //Code adapted from http://invisible-island.net/ncurses/ncurses-intro.html  #include <cassert> #include <cstdlib> #include <csignal>  #include "curses.h"  static void finish(int sig);  int main() {   std::signal(SIGINT, finish);   initscr();   keypad(stdscr, TRUE);   cbreak();    int x = 0;   int y = 0;    while (1)   {     move(y,x);     refresh();     const int c = getch();     switch (c)     {       case KEY_UP   : y-=(y-1>   0  ? 1 : 0); break;       case KEY_RIGHT: x+=(x+1<COLS  ? 1 : 0); break;       case KEY_DOWN : y+=(y+1<LINES ? 1 : 0); break;       case KEY_LEFT : x-=(x-1>   0  ? 1 : 0); break;       default: addch(c); x+=(x+1<COLS  ? 1 : 0); break;     }   }   finish(0); }  static void finish(int sig) {   endwin();   std::exit(sig); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)