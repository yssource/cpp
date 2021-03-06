
 

 

 

 

 

([C++](Cpp.md)) [ArrayExample4](CppArrayExample4.md)
======================================================

 

![STL](PicStl.png)

 

[Array example 4](CppArrayExample4.md) is an [array](CppArray.md)
[example](CppExample.md).

Technical facts
---------------

 

[Application type(s)](CppApplication.md)

-   ![Desktop](PicDesktop.png) [Desktop
    application](CppDesktopApplication.md)

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1

[Project type](CppQtProjectType.md):

-   ![GUI](PicGui.png) [GUI application](CppGuiApplication.md)

[C++ standard](CppStandard.md):

-   ![C++11](PicCpp11.png) [C++11](Cpp11.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![Qt](PicQt.png) [Qt](CppQt.md): version 5.4.1 (32 bit)
-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppArrayExample4/CppArrayExample4.pro
--------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` exists (../../ConsoleApplication.pri) {   include(../../ConsoleApplication.pri) } !exists (../../ConsoleApplication.pri) {   QT += core   QT += gui   greaterThan(QT_MAJOR_VERSION, 4): QT += widgets   CONFIG   += console   CONFIG   -= app_bundle   TEMPLATE = app   CONFIG(release, debug|release) {     DEFINES += NDEBUG NTRACE_BILDERBIKKEL   }   QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++   unix {     QMAKE_CXXFLAGS += -Werror   } }  exists(../../Libraries/Boost.pri) {   include(../../Libraries/Boost.pri) } !exists(../../Libraries/Boost.pri) {   win32 {     INCLUDEPATH += \       ../../Libraries/boost_1_55_0   } }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppArrayExample4/main.cpp
---------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cstdlib> #include <vector>  #include <iostream> #include <string>  #include <boost/date_time/posix_time/ptime.hpp> #include <boost/date_time/microsec_time_clock.hpp>  //#define USE_ORIGINAL #define USE_IMPROVED   class TestTimer { public:     TestTimer(const std::string & name) : name(name),         start(boost::date_time::microsec_clock<boost::posix_time::ptime>::local_time())     {     }      ~TestTimer()     {         using namespace std;         using namespace boost;          posix_time::ptime now(date_time::microsec_clock<posix_time::ptime>::local_time());         posix_time::time_duration d = now - start;          cout << name << " completed in " << d.total_milliseconds() / 1000.0 <<             " seconds" << endl;     }  private:     std::string name;     boost::posix_time::ptime start; };  struct Pixel {     Pixel(unsigned char r = 0, unsigned char g = 0, unsigned char b = 0) : r(r), g(g), b(b)     {     }      unsigned char r, g, b; };  void UseVector() {     TestTimer t("UseVector");      for(int i = 0; i < 1000; ++i)     {         int dimension = 999;          #ifdef USE_ORIGINAL         std::vector<Pixel> pixels;         pixels.resize(dimension * dimension);         for(int i = 0; i < dimension * dimension; ++i)         {             pixels[i].r = 255;             pixels[i].g = 0;             pixels[i].b = 0;         }         #endif // USE_ORIGINAL         #ifdef USE_IMPROVED         std::vector<Pixel> pixels(dimension * dimension, Pixel(255,0,0));         #endif     } }  void UseVectorPushBack() {     TestTimer t("UseVectorPushBack");      for(int i = 0; i < 1000; ++i)     {         int dimension = 999;          std::vector<Pixel> pixels;         pixels.reserve(dimension * dimension);          for(int i = 0; i < dimension * dimension; ++i)             pixels.push_back(Pixel(255, 0, 0));     } }  void UseArray() {     TestTimer t("UseArray");      for(int i = 0; i < 1000; ++i)     {         int dimension = 999;          Pixel * pixels = (Pixel *)malloc(sizeof(Pixel) * dimension * dimension);          for(int i = 0 ; i < dimension * dimension; ++i)         {             pixels[i].r = 255;             pixels[i].g = 0;             pixels[i].b = 0;         }          free(pixels);     } }  int main() {     TestTimer t1("The whole thing");      UseArray();     UseVector();     UseVectorPushBack();      return 0; }  /* When #define USE_ORIGINAL in debug mode  UseArray completed in 6.191 seconds UseVector completed in 44.706 seconds UseVectorPushBack completed in 63.059 seconds The whole thing completed in 113.957 seconds  */  /* When #define USE_IMPROVED in debug mode  UseArray completed in 6.965 seconds UseVector completed in 19.794 seconds UseVectorPushBack completed in 66.436 seconds The whole thing completed in 93.197 seconds  */  /* When #define USE_IMPROVED in release mode  UseArray completed in 2.438 seconds UseVector completed in 2.437 seconds UseVectorPushBack completed in 11.672 seconds The whole thing completed in 16.548 seconds  */`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

