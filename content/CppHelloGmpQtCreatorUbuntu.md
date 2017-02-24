



 

 

 

 

 

([C++](Cpp.htm)) ['Hello GMP' using Qt Creator under Ubuntu](CppHelloGmpQtCreatorUbuntu.htm)
============================================================================================

 

![Qt Creator](PicQtCreator.png)![Ubuntu](PicUbuntu.png)

 

[Hello GMP](CppHelloGmp.htm) using [Qt Creator](CppQtCreator.htm) under
Ubuntu is straightforward: just run the project.

 

-   [Download the Qt Creator project 'Hello GMP' (zip)](CppHelloGmp.zip)

 

Operating system: [Ubuntu](http://www.ubuntu.com) 10.04 LTS Lucid Lynx

[IDE](CppIde.htm): [Qt Creator](CppQtCreator.htm) 2.0.0

[Project type](CppQtProjectType.htm): console application

[Compiler](CppCompiler.htm): [G++](CppGpp.htm) 4.4.1

[Libraries](CppLibrary.htm) used:

-   [GMP](CppGmp.htm): version 5.0.1

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm)
---------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #------------------------------------------------- # # Project created by QtCreator 2010-10-01T08:45:31 # #------------------------------------------------- QT       += core QT       -= gui TARGET = CppHelloGmp unix:LIBS+= -L/usr/lib -lgmp CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

main.cpp
--------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <gmpxx.h>  ///From http://www.richelbilderbeek.nl/CppMpz_tToStr.htm const std::string Mpz_tToStr(const mpz_t& i) {   static char buffer[256];   mpz_get_str(buffer,10,i);   return std::string(buffer); }  int main() {   mpz_t i;   mpz_init_set_str(i,"123456789012345678901234567890",10);   //Perform i = i * i   mpz_mul(i,i,i);    std::cout     << "Hello GMP,\n"     << Mpz_tToStr(i) << " times.\n";    mpz_clear(i); } `
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)