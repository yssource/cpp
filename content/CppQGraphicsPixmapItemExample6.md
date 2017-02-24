



 

 

 

 

 

([C++](Cpp.htm)) [QGraphicsPixmapItemExample6](CppQGraphicsPixmapItemExample6.htm)
==================================================================================

 

[QGraphicsPixmapItem example 6: let the view respond to cursor moving
over pixmap](CppQGraphicsPixmapItemExample6.htm) is a
[QGraphicsPixmapItem](CppQGraphicsPixmapItem.htm) example. This example
shows how to let the [QGraphicsView](CppQGraphicsView.png) responds to
the cursor being moved over the
[QGraphicsPixmapItem](CppQGraphicsPixmapItem.htm).

 

-   [View a screenshot of
    'CppQGraphicsPixmapItemExample6' (png)](CppQGraphicsPixmapItemExample6.png)
-   ![Qt Creator](PicQtCreator.png) [Download the Qt Creator project
    'CppQGraphicsPixmapItemExample6' (zip)](CppQGraphicsPixmapItemExample6.zip)

 

[QGraphicsPixmapItem example 6: let the view respond to cursor moving
over pixmap](CppQGraphicsPixmapItemExample6.htm) is the predecessor of
[QGraphicsPixmapItem example 7: respond to cursor moving over pixmap
while holding the cursor still](CppQGraphicsPixmapItemExample7.htm).

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppQGraphicsPixmapItemExample6/CppQGraphicsPixmapItemExample6.pro
------------------------------------------------------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` exists (../../DesktopApplication.pri) {   include(../../DesktopApplication.pri) } !exists (../../DesktopApplication.pri) {   QT += core printsupport   QT += gui   greaterThan(QT_MAJOR_VERSION, 4): QT += widgets svg   CONFIG   += console   CONFIG   -= app_bundle   TEMPLATE = app   CONFIG(release, debug|release) {     DEFINES += NDEBUG NTRACE_BILDERBIKKEL   }   QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++   unix {     QMAKE_CXXFLAGS += -Werror   } }  exists(../../Libraries/Boost.pri) {   include(../../Libraries/Boost.pri) } !exists(../../Libraries/Boost.pri) {   win32 {     INCLUDEPATH += \       ../../Libraries/boost_1_55_0   } }  SOURCES += \     qtmain.cpp \     qtwidget.cpp \     qtitem.cpp  HEADERS += \     qtwidget.h \     qtitem.h  RESOURCES += \     CppQGraphicsPixmapItemExample6.qrc`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQGraphicsPixmapItemExample6/qtitem.h
-----------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTITEM_H #define QTITEM_H  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include <QGraphicsPixmapItem> #pragma GCC diagnostic pop  ///A QGraphicsPixmapItem that loads its pixmap from resources ///and is clickable struct QtItem : public QGraphicsPixmapItem {   QtItem(QGraphicsItem *parent = 0);    protected:   void paint(QPainter *painter, const QStyleOptionGraphicsItem *option, QWidget *widget); };  #endif // QTITEM_H`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQGraphicsPixmapItemExample6/qtitem.cpp
-------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include <cassert> #include <QCursor> #include <QPainter> #include "qtitem.h" #pragma GCC diagnostic pop  QtItem::QtItem(QGraphicsItem *parent)   : QGraphicsPixmapItem(parent) {   assert(this->pixmap().isNull()     && "Assume no pixmap loaded yet");    //Load the pixmap from resources   this->setPixmap(QPixmap(":/images/PicR.png"));    assert(!this->pixmap().isNull()     && "Assume pixmap is loaded successfully");    //Let the item have (0.0,0.0) as its center,   //so it will remain in place when rotating   this->setOffset(-pixmap().rect().center());    this->setFlags(       QGraphicsItem::ItemIsMovable     | QGraphicsItem::ItemIsSelectable);  }  void QtItem::paint(QPainter *painter, const QStyleOptionGraphicsItem *option, QWidget *widget) {   //Let QGraphicsPixmapItem handle most of the painting   QGraphicsPixmapItem::paint(painter,option,widget);    //Draw a thick red line around the pixmap when it is selected   if (this->isSelected())   {     painter->setPen(QPen(QColor(255,0,0),3));     painter->drawRoundedRect(this->boundingRect().adjusted(3.0,3.0,-3.0,-3.0),6.0,6.0);   } }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQGraphicsPixmapItemExample6/qtmain.cpp
-------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include <QApplication> #include "qtwidget.h" #pragma GCC diagnostic pop  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   QtWidget w;   w.setGeometry(100,100,400,400);   w.show();   return a.exec(); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQGraphicsPixmapItemExample6/qtwidget.h
-------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTWIDGET_H #define QTWIDGET_H  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include <QGraphicsView> #pragma GCC diagnostic pop  ///Forward declaration struct QtItem;  struct QtWidget : public QGraphicsView {   QtWidget();    protected:   void mouseMoveEvent(QMouseEvent *event); };  #endif // QTWIDGET_H`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQGraphicsPixmapItemExample6/qtwidget.cpp
---------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include <cassert> #include <iostream>  #include <boost/bind.hpp> #include <boost/lambda/bind.hpp>  #include <QGraphicsScene> #include <QGraphicsPixmapItem> #include <QMouseEvent>  #include "qtitem.h" #include "qtwidget.h" #pragma GCC diagnostic pop  QtWidget::QtWidget() {   QGraphicsScene * const scene = new QGraphicsScene(this);   this->setScene(scene);   const int n_items = 8;   for (int i=0; i!=n_items; ++i)   {     QtItem * const item = new QtItem;     //Scatter those items around a bit     item->setPos(       - 128 + (std::rand() % 256),       - 128 + (std::rand() % 256));      scene->addItem(item);   }    ///Without this line, mouseMoveEvent will not be called   this->setMouseTracking(true); }  void QtWidget::mouseMoveEvent(QMouseEvent *event) {   //Rotate the first item found under the cursor   {     //Find the items under the cursor     QList<QGraphicsItem *> all_items = this->scene()->items();     std::vector<QGraphicsItem *> items; //The items under the cursor     const QPointF pos = this->mapToScene(event->pos());      std::for_each(all_items.begin(),all_items.end(),       [this,&items,pos](QGraphicsItem * item)       {         const QRectF rect = item->boundingRect().translated(item->pos());         if (rect.contains(pos))         {           items.push_back(item);         }       }     );     //Rotate the possible first item found     if (!items.empty())     {       QGraphicsItem * const item = items[0];       item->setRotation(item->rotation() + 10.0);       item->update();     }   }    //Let QGraphicsView handle the default mouseMoveEvents, for example   //the moving of the items   QGraphicsView::mouseMoveEvent(event); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)