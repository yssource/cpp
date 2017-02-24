



 

 

 

 

 

([C++](Cpp.htm)) [BoostGeometryExample7](CppBoostGeometryExample7.htm)
======================================================================

 

![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[Boost.Geometry example 7: Bug in
boost::geometry::convex\_hull](CppBoostGeometryExample7.htm) is a
[Boost.Geometry](CppBoostGeometry.htm) [example](CppExample.htm).

Technical facts
---------------

 

[Application type(s)](CppApplication.htm)

-   ![Desktop](PicDesktop.png) [Desktop
    application](CppDesktopApplication.htm)

[Operating system(s) or programming environment(s)](CppOs.htm)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.htm) 15.04 (vivid)

[IDE(s)](CppIde.htm):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.htm) 3.1.1

[Project type](CppQtProjectType.htm):

-   ![GUI](PicGui.png) [GUI application](CppGuiApplication.htm)

[C++ standard](CppStandard.htm):

-   ![C++11](PicCpp11.png) [C++11](Cpp11.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.9.2

[Libraries](CppLibrary.htm) used:

-   ![Qt](PicQt.png) [Qt](CppQt.htm): version 5.4.1 (32 bit)
-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppBoostGeometryExample7/CppBoostGeometryExample7.pro
------------------------------------------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` exists(../../ConsoleApplication.pri) {   include(../../ConsoleApplication.pri) } !exists(../../ConsoleApplication.pri) {   QT += core   QT += gui   greaterThan(QT_MAJOR_VERSION, 4): QT += widgets   CONFIG   += console   CONFIG   -= app_bundle   TEMPLATE = app   CONFIG(release, debug|release) {     DEFINES += NDEBUG NTRACE_BILDERBIKKEL   }   QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++   unix {     QMAKE_CXXFLAGS += -Werror   } }  exists(../../Libraries/Boost.pri) {   include(../../Libraries/Boost.pri) } !exists(../../Libraries/Boost.pri) {   win32 {     INCLUDEPATH += \       ../../Libraries/boost_1_55_0   } }  SOURCES += main.cpp`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostGeometryExample7/main.cpp
-----------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <iostream>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-variable" #include <boost/geometry.hpp> #include <boost/geometry/geometries/point_xy.hpp> #pragma GCC diagnostic pop  //Goal: determine if a polygon, derived from points, is convex //Member function: if the convex_hull equals that points, it is convex // //Bug: convex_hull does make a convex polygon look concave for certain values // //Bug report is posted at https://svn.boost.org/trac/boost/ticket/9873 int main() {   using namespace boost::geometry;   typedef model::d2::point_xy<double> Point;   typedef model::polygon<Point> Polygon;    //Example A: works as expected   {     /* Polygon used:        -       |       -  2---3       |  |       -  1---0       |       +--|---|---|      (point values are those simplified from example B)      */     const std::vector<Point> points {         {15.0,631.0},         { 8.0,628.0},         { 8.0,679.0},         {15.0,682.0}     };      Polygon polygon;     append(polygon, points);      assert(boost::geometry::num_points(polygon) == 4);      boost::geometry::correct(polygon);      assert(boost::geometry::num_points(polygon) == 5       && "OK: boost::geometry::correct adds a point");      Polygon hull;     boost::geometry::convex_hull(polygon, hull);      assert(boost::geometry::num_points(hull) == 5       && "OK: the hull of a convex polygon has the same number of points as that polygon");     assert(boost::geometry::equals(polygon,hull));   }    //Example B: does not work as expected   {     /* Polygon used:        -       |       -  2---3       |  |       -  1---0       |       +--|---|---|       */     const std::vector<Point> points {         {15.9835,631.923},         {8.24075,628.579},         {8.24075,679.58 },         {15.9835,682.926}     };      Polygon polygon;     append(polygon, points);     assert(boost::geometry::num_points(polygon) == 4);      boost::geometry::correct(polygon);      assert(boost::geometry::num_points(polygon) == 5       && "OK: boost::geometry::correct adds a point");      Polygon hull;     boost::geometry::convex_hull(polygon, hull);      assert(boost::geometry::num_points(hull) == 6       && "Should not add an extra point, as the original polygon was convex");      assert(!boost::geometry::equals(polygon,hull)       && "Should be equal, but does not");   } }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)