
 

 

 

 

 

([C++](Cpp.md)) [QtExample34](CppQtExample34.md)
==================================================

 

![Qt](PicQt.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[Qt example 34: moveable, selectable and editable
arrows](CppQtExample34.md) is a [Qt example](CppQtExample.md) to
create some arrows that are (easily) selectable, moveable and editable.
Arrows can be edited by mouse press and a keyboard press: whil holding
shift, click the end of an arrow to have an arrowhead added or removed.
When having selected an arrow, press 1,F1,the minus sign of 't' to have
the tail arrowhead added or removed. Or, when having selected an arrow,
press 2,F2,the plus sign of 'h' to have the head arrowhead added or
removed.

 

What I liked, is that it is possible to select multiple items while
holding CTRL (which is standard GUI behavior) and edit these all at the
same time using a key press!

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppQtExample34/CppQtExample34.pro
----------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` exists(../../DesktopApplication.pri) {   include(../../DesktopApplication.pri) } !exists(../../DesktopApplication.pri) {   QT += core gui   greaterThan(QT_MAJOR_VERSION, 4): QT += widgets   TEMPLATE = app    CONFIG(debug, debug|release) {     message(Debug mode)   }    CONFIG(release, debug|release) {     message(Release mode)     DEFINES += NDEBUG NTRACE_BILDERBIKKEL   }    QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra    unix {     QMAKE_CXXFLAGS += -Werror   } }  exists(../../Libraries/Boost.pri) {   include(../../Libraries/Boost.pri) } !exists(../../Libraries/Boost.pri) {   win32 {     INCLUDEPATH += \       ../../../Projects/Libraries/boost_1_55_0   } }  SOURCES += \     qtmain.cpp \     qtarrowswidget.cpp \     qtarrowitem.cpp  HEADERS += \     qtarrowswidget.h \     qtarrowitem.h`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample34/qtarrowitem.h
------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTARROWITEM_H #define QTARROWITEM_H  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <QGraphicsLineItem> #pragma GCC diagnostic pop  struct QtArrowItem : public QGraphicsLineItem {   QtArrowItem(     const double x1,     const double y1,     const bool tail,     const double x2,     const double y2,     const bool head,     QGraphicsItem *parent = 0);    ///Respond to key presses   void keyPressEvent(QKeyEvent *event);    protected:   ///The rectangle that containg the item, used for rough calculations like   ///collision detection   QRectF boundingRect() const;     ///Respond to mouse press   void mousePressEvent(QGraphicsSceneMouseEvent *event);    ///Paint a QtTextPositionItem   void paint(QPainter *painter, const QStyleOptionGraphicsItem *, QWidget *);    ///More precise shape compared to boundingRect   ///In this example, it is redefined to ease selecting those thin lines   QPainterPath shape() const;     private:   ///The extra width given to the line for easier clicking   static const double m_click_easy_width;    ///Show arrow at head   bool m_head;    ///Show arrow at tail   bool m_tail;    ///Obtain the angle in radians between two deltas   ///12 o'clock is 0.0 * pi   /// 3 o'clock is 0.5 * pi   /// 6 o'clock is 1.0 * pi   /// 9 o'clock is 1.5 * pi   //From www.richelbilderbeek.nl/CppGetAngle.htm   static double GetAngle(const double dx, const double dy);  };  #endif // QTARROWITEM_H`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample34/qtarrowitem.cpp
--------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <cmath>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/math/constants/constants.hpp>  #include <QGraphicsSceneMouseEvent> #include <QKeyEvent> #include <QPainter>  #include "qtarrowitem.h" #pragma GCC diagnostic pop  const double QtArrowItem::m_click_easy_width = 10.0;  QtArrowItem::QtArrowItem(   const double x1,   const double y1,   const bool tail,   const double x2,   const double y2,   const bool head,   QGraphicsItem *parent)   : QGraphicsLineItem(x1,y1,x2,y2,parent),     m_head(head),     m_tail(tail) {   this->setFlag(QGraphicsItem::ItemIsMovable);   this->setFlag(QGraphicsItem::ItemIsSelectable);   assert(this->line().p1() == QPointF(x1,y1));   assert(this->line().p2() == QPointF(x2,y2)); }  double QtArrowItem::GetAngle(const double dx, const double dy) {   return boost::math::constants::pi<double>() - (std::atan(dx/dy)); }  QRectF QtArrowItem::boundingRect() const {   return shape().boundingRect(); }  void QtArrowItem::keyPressEvent(QKeyEvent *event) {   switch (event->key())   {     case Qt::Key_F1:     case Qt::Key_1:     case Qt::Key_T:     case Qt::Key_Minus:       m_tail = !m_tail;       this->update();       break;     case Qt::Key_F2:     case Qt::Key_2:     case Qt::Key_H:     case Qt::Key_Plus:       m_head = !m_head;       this->update();       break;     default:       break;   } }  void QtArrowItem::mousePressEvent(QGraphicsSceneMouseEvent *event) {   if (event->modifiers() & Qt::ShiftModifier)   {     if ((event->pos() - this->line().p1()).manhattanLength() < 10.0)     {       m_tail = !m_tail;       this->update();     }     else if ((event->pos() - this->line().p2()).manhattanLength() < 10.0)     {       m_head = !m_head;       this->update();     }   } }  void QtArrowItem::paint(QPainter *painter, const QStyleOptionGraphicsItem *, QWidget *) {   painter->setRenderHint(QPainter::Antialiasing);   if (this->isSelected())   {     const QColor color(255,0,0);     QPen pen;     pen.setColor(color);     pen.setWidth(3);     painter->setPen(pen);     QBrush brush;     brush.setColor(color);     brush.setStyle(Qt::SolidPattern);     painter->setBrush(brush);   }   else   {     const QColor color(0,0,0);     QPen pen;     pen.setColor(color);     pen.setWidth(1);     painter->setPen(pen);     QBrush brush;     brush.setColor(color);     brush.setStyle(Qt::SolidPattern);     painter->setBrush(brush);   }   painter->drawLine(this->line());    //The angle from tail to head   double angle = GetAngle(line().dx(),line().dy());   if (line().dy() >= 0.0) angle = (1.0 * boost::math::constants::pi<double>()) + angle;   const double sz = 10.0; //pixels   if (m_tail)   {     const QPointF p0 = this->line().p1();     const QPointF p1       = p0 + QPointF(          std::sin(angle + boost::math::constants::pi<double>() + (boost::math::constants::pi<double>() * 0.1)) * sz,         -std::cos(angle + boost::math::constants::pi<double>() + (boost::math::constants::pi<double>() * 0.1)) * sz);     const QPointF p2       = p0 + QPointF(          std::sin(angle + boost::math::constants::pi<double>() - (boost::math::constants::pi<double>() * 0.1)) * sz,         -std::cos(angle + boost::math::constants::pi<double>() - (boost::math::constants::pi<double>() * 0.1)) * sz);     painter->drawPolygon(QPolygonF() << p0 << p1 << p2);   }   if (m_head)   {     const QPointF p0 = this->line().p2();      const QPointF p1       = p0 + QPointF(          std::sin(angle +  0.0 + (boost::math::constants::pi<double>() * 0.1)) * sz,         -std::cos(angle +  0.0 + (boost::math::constants::pi<double>() * 0.1)) * sz);     const QPointF p2       = p0 + QPointF(          std::sin(angle +  0.0 - (boost::math::constants::pi<double>() * 0.1)) * sz,         -std::cos(angle +  0.0 - (boost::math::constants::pi<double>() * 0.1)) * sz);      painter->drawPolygon(QPolygonF() << p0 << p1 << p2);   } }  QPainterPath QtArrowItem::shape() const {   //Thanks to norobro for posting this code at   //http://www.qtcentre.org/threads/49201-Increase-margin-for-detecting-tooltip-events-of-QGraphicsLineItem   QPainterPath path;   QPainterPathStroker stroker;   path.moveTo(line().p1());   path.lineTo(line().p2());   stroker.setWidth(m_click_easy_width);   return stroker.createStroke(path); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample34/qtarrowswidget.h
---------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTARROWSWIDGET_H #define QTARROWSWIDGET_H  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <QGraphicsView> #pragma GCC diagnostic pop  struct QtArrowsWidget : public QGraphicsView {   QtArrowsWidget();    protected:   ///Respond to a key press   void keyPressEvent(QKeyEvent *event);    private:   ///The QGraphicsScene working on   QGraphicsScene * const m_scene; };  #endif // QTARROWSWIDGET_H`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample34/qtarrowswidget.cpp
-----------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/math/constants/constants.hpp>  #include <QGraphicsScene> #include <QGraphicsPixmapItem>  #include "qtarrowitem.h" #include "qtarrowswidget.h" #pragma GCC diagnostic pop  QtArrowsWidget::QtArrowsWidget()   : m_scene(new QGraphicsScene(this)) {    this->setScene(m_scene);   const int n_arrows = 16;   for (int i=0; i!=n_arrows; ++i)   {     const double angle = 2.0 * boost::math::constants::pi<double>() * (static_cast<double>(i) / static_cast<double>(n_arrows));     const double x1 =  std::sin(angle) * 100.0;     const double y1 = -std::cos(angle) * 100.0;     const bool tail = (std::rand() >> 4) % 2;     const double x2 =  std::sin(angle) * 200.0;     const double y2 = -std::cos(angle) * 200.0;     const bool head = (std::rand() >> 4) % 2;      QtArrowItem * item = new QtArrowItem(x1,y1,tail,x2,y2,head);     m_scene->addItem(item);   } }  void QtArrowsWidget::keyPressEvent(QKeyEvent *event) {   const QList<QGraphicsItem *> v = m_scene->selectedItems();   std::for_each(v.begin(),v.end(),     [event](QGraphicsItem * item)     {       if (QtArrowItem * const arrow = dynamic_cast<QtArrowItem*>(item))       {         arrow->keyPressEvent(event);       }     }   ); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample34/qtmain.cpp
---------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <QApplication> #include <QDesktopWidget> #include "qtarrowswidget.h" #pragma GCC diagnostic pop  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   QtArrowsWidget w;   {     //Resize the dialog and put it in the screen center     w.setGeometry(0,0,600,400);     const QRect screen = QApplication::desktop()->screenGeometry();     w.move( screen.center() - w.rect().center() );   }   w.show();   return a.exec(); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

