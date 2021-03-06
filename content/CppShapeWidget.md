
 

 

 

 

 

([C++](Cpp.md)) [ShapeWidget](CppShapeWidget.md)
==================================================

 

![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[ShapeWidget](CppShapeWidget.md) is a [widget](CppWidget.md)
[class](CppClass.md) for a [Shape](CppShape.md).

Technical facts
---------------

 

 

 

 

 

 

./CppShapeWidget/CppShapeWidget.pri
-----------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppShapeWidget  SOURCES += \     ../../Classes/CppShapeWidget/shapewidget.cpp  HEADERS  += \     ../../Classes/CppShapeWidget/shapewidget.h  OTHER_FILES += \     ../../Classes/CppShapeWidget/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppShapeWidget/shapewidget.h
------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* ShapeWidget, class for displaying a Shape Copyright 2011-2015 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program. If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppShapeWidget.htm //--------------------------------------------------------------------------- #ifndef SHAPEWIDGET_H #define SHAPEWIDGET_H  #include <string> #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/checked_delete.hpp> #include <boost/signals2.hpp> #include "widget.h" #pragma GCC diagnostic pop  namespace ribi {  struct Shape;  ///ShapeWidget is a class to display a Shape struct ShapeWidget : public Widget {   explicit ShapeWidget(     const int n_corners,     const double rotation,     const int x = 0,     const int y = 0,     const int width = 100,     const int height = 100,     const unsigned char red = 255,     const unsigned char green = 255,     const unsigned char blue = 255);    ///Make a deep copy of ShapeWidget   ShapeWidget * Clone() const noexcept;    ///Obtain a read-only pointert to the Shape   const Shape * GetShape() const noexcept { return m_shape.get(); }     private:   //ShapeWidget can only be deleted by Boost smart pointers   virtual ~ShapeWidget() noexcept {}   friend void boost::checked_delete<>(ShapeWidget*);   friend bool operator==(const ShapeWidget& lhs,const ShapeWidget& rhs) noexcept;    ///The Shape   boost::scoped_ptr<Shape> m_shape;    public:   static std::string GetVersion() noexcept;   static std::vector<std::string> GetVersionHistory() noexcept; };  bool operator==(const ShapeWidget& lhs,const ShapeWidget& rhs) noexcept;  } //~namespace ribi  #endif // SHAPEWIDGET_H`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppShapeWidget/shapewidget.cpp
--------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include "shapewidget.h"  #include <cassert> #include <cmath>  #include <boost/numeric/conversion/cast.hpp>  #include "shape.h"  //#include "trace.h"  #pragma GCC diagnostic pop  ribi::ShapeWidget::ShapeWidget(   const int n_corners,   const double rotation,   const int x,   const int y,   const int width,   const int height,   const unsigned char red,   const unsigned char green,   const unsigned char blue)   : m_shape(new Shape(n_corners,rotation,red,green,blue)) {   SetGeometry(x,y,width,height); }  ribi::ShapeWidget * ribi::ShapeWidget::Clone() const noexcept {   ShapeWidget * const w = new ShapeWidget(     GetShape()->GetNumberOfCorners(),     GetShape()->GetRotation(),     GetLeft(),     GetTop(),     GetWidth(),     GetHeight(),     GetShape()->GetRed(),     GetShape()->GetGreen(),     GetShape()->GetBlue()   );   assert(*w == *this);   return w; }  std::string ribi::ShapeWidget::GetVersion() noexcept {   return "2.1"; }  std::vector<std::string> ribi::ShapeWidget::GetVersionHistory() noexcept {   return {     "2011-07-13: Version 1.0: initial version",     "2011-07-18: Version 1.1: removed useless member functions",     "2011-08-08: Version 2.0: conformized architecture to MysteryMachineWidget",     "2014-03-28: version 2.1: replaced Rect by Boost.Geometry its box class"   }; }  bool ribi::operator==(const ShapeWidget& lhs,const ShapeWidget& rhs) noexcept {   return     //lhs.GetGeometry() ==  rhs.GetGeometry()     //&&     *lhs.GetShape()    == *rhs.GetShape(); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

