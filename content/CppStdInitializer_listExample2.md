
 

 

 

 

 

([C++](Cpp.md)) [StdInitializer\_listExample2](CppStdInitializer_listExample2.md)
===================================================================================

 

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppStdInitializer\_listExample2/CppStdInitializer\_listExample2.pro
--------------------------------------------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  SOURCES += main.cpp`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStdInitializer\_listExample2/main.cpp
------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <array> #include <cassert> #include <initializer_list> #include <tuple> #include <vector>  struct MyArray {   MyArray(const std::initializer_list<int>& v)     : m_v(ToArray(v))   {    }    static std::array<int,4> ToArray(const std::initializer_list<int>& v)   {     if (v.size() != 4)     {       throw std::logic_error("MyArray must be initialized with std::initializer_list with size 4");     }     std::array<int,4> a;     std::copy(std::begin(v),std::end(v),std::begin(a));     return a;   }   const std::array<int,4> m_v; };  struct MyTuple {   MyTuple(const std::initializer_list<int>& v)     : m_v{ToTuple(v)} {}    template <int I>   int Get() const noexcept   {     return std::get<I>(m_v);   }    static std::tuple<int,int,int,int> ToTuple(const std::initializer_list<int>& v)   {     if (v.size() != 4)     {       throw std::logic_error("MyTuple must be initialized with std::initializer_list with size 4");     }     return std::make_tuple(       *(v.begin()+0),       *(v.begin()+1),       *(v.begin()+2),       *(v.begin()+3)     );   }    const std::tuple<int,int,int,int> m_v; };  struct MyVector {   MyVector(const std::initializer_list<int>& v) : m_v{v} {}   const std::vector<int> m_v; };  int main() {   const MyArray a( {1,2,3,4} );   assert(a.m_v[0] == 1);   assert(a.m_v[1] == 2);   assert(a.m_v[2] == 3);   assert(a.m_v[3] == 4);    const MyTuple t( {1,2,3,4} );   assert(t.Get<0>() == 1);   assert(t.Get<1>() == 2);   assert(t.Get<2>() == 3);   assert(t.Get<3>() == 4);   //assert(t.Get<4>() == 4); //Won't compile    const MyVector v( {1,2,3,4} );   assert(v.m_v[0] == 1);   assert(v.m_v[1] == 2);   assert(v.m_v[2] == 3);   assert(v.m_v[3] == 4);  }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

