
 

 

 

 

 

([C++](Cpp.md)) [StdTr1ArrayExample1](CppStdTr1ArrayExample1.md)
==================================================================

 

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1

[Project type](CppQtProjectType.md):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)

[C++ standard](CppStandard.md):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppStdTr1ArrayExample1/CppStdTr1ArrayExample1.pro
--------------------------------------------------------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------
  ` TEMPLATE = app CONFIG += console CONFIG -= app_bundle CONFIG -= qt  SOURCES += main.cpp  #QMAKE_CXXFLAGS += -std=c++11`
  ---------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStdTr1ArrayExample1/main.cpp
---------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <tr1/array> #include <cassert>  int main() {   const int sz = 3;   std::tr1::array<int,sz> v;   v[0] = 0;   v[1] = 1;   v[2] = 2;   assert(v.size() == sz);   assert(v[0] == 0);   assert(v[1] == 1);   assert(v[2] == 2); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

