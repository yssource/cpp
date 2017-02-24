



 

 

 

 

 

([C++](Cpp.htm)) [RpiExample1](CppRpiExample1.htm)
==================================================

 

![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Raspbian](PicRaspbian.png)

 

[Raspberry Pi example 1: toggle all GPIO pins on and
off](CppRpiExample1.htm) is a [Raspberry Pi](CppRpi.htm) example to
toggle all GPIO pins on and off.

 

-   [Download the Qt Creator project
    'CppRpiExample1' (zip)](CppRpiExample1.zip)

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

-   ![C++11](PicCpp11.png) [C++11](Cpp11.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.9.2

[Libraries](CppLibrary.htm) used:

-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppRpiExample1/CppRpiExample1.pro
----------------------------------------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------
  ` TEMPLATE = app CONFIG += console CONFIG -= qt QMAKE_CXXFLAGS += -std=c++0x SOURCES += main.cpp DEFINES += NDEBUG`
  ---------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppRpiExample1/main.cpp
-------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <iostream> #include <boost/lexical_cast.hpp> #include <boost/timer.hpp>  //Toggles all GPIO pins every second //Thanks to http://www.cl.cam.ac.uk/freshers/raspberrypi/tutorials/temperature/#step-six  int main() {   const std::vector<int> gpios = { 2,3,4,7,8,9,10,11,14,15,17,18,22,23,24,25,27 };    while (1)   {     //Set all GPIO pins high     for(int i: gpios)     {       {         const std::string cmd = "echo \"" + boost::lexical_cast<std::string>(i) + "\" > /sys/class/gpio/export";         std::clog << cmd << '\n';         const int error = std::system(cmd.c_str());         assert(!error);       }       {         const std::string cmd = "echo \"out\" > /sys/class/gpio/gpio" + boost::lexical_cast<std::string>(i)+ "/direction";         std::clog << cmd << '\n';         const int error = std::system(cmd.c_str());         assert(!error);       }       {         const std::string cmd = "echo \"1\" > /sys/class/gpio/gpio" + boost::lexical_cast<std::string>(i)+ "/value";         std::clog << cmd << '\n';         const int error = std::system(cmd.c_str());         assert(!error);       }     }     //Wait a second     {       boost::timer t;       while (t.elapsed() < 1.0) {}     }     //Set all GPIO pins low     for(int i: gpios)     {       {         const std::string cmd = "echo \"0\" > /sys/class/gpio/gpio" + boost::lexical_cast<std::string>(i)+ "/value";         std::clog << cmd << '\n';         const int error = std::system(cmd.c_str());         assert(!error);       }       {         const std::string cmd = "echo \"" + boost::lexical_cast<std::string>(i) + "\" > /sys/class/gpio/unexport";         std::clog << cmd << '\n';         const int error = std::system(cmd.c_str());         assert(!error);       }     }     //Wait a second     {       boost::timer t;       while (t.elapsed() < 1.0) {}     }   }  }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)