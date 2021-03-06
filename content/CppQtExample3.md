
 

 

 

 

 

([C++](Cpp.md)) [QtExample3](CppQtExample3.md)
================================================

 

![Qt](PicQt.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)![Ubuntu](PicUbuntu.png)

 

[Qt example 3: a changing background in 2D](CppQtExample3.md) is a [Qt
example](CppQtExample.md) that shows a changing background in 2D, like
[this screenshot (png)](CppQtExample3.png).

 

-   [Download the Qt Creator project file
    'CppQtExample3' (zip)](CppQtExample3.zip)

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppQtExample3/CppQtExample3.pro
--------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` exists(../../DesktopApplication.pri) {   include(../../DesktopApplication.pri) } !exists(../../DesktopApplication.pri) {   QT += core gui   greaterThan(QT_MAJOR_VERSION, 4): QT += widgets   TEMPLATE = app    CONFIG(debug, debug|release) {     message(Debug mode)   }    CONFIG(release, debug|release) {     message(Release mode)     DEFINES += NDEBUG NTRACE_BILDERBIKKEL   }    QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra    unix {     QMAKE_CXXFLAGS += -Werror   } }  exists(../../Libraries/Boost.pri) {   include(../../Libraries/Boost.pri) } !exists(../../Libraries/Boost.pri) {   win32 {     INCLUDEPATH += \       ../../../Projects/Libraries/boost_1_55_0   } }  SOURCES += main.cpp`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample3/main.cpp
------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/shared_ptr.hpp> #include <QApplication> #include <QDesktopWidget> #include <QGraphicsPixmapItem> #include <QGraphicsScene> #include <QGraphicsView> #include <QTimer> #pragma GCC diagnostic pop  struct ChangingBackground : public QGraphicsPixmapItem {   ChangingBackground(const int width, const int height)     : z(0)   {     QPixmap m(width,height);     this->setPixmap(m);   }   void advance(int)   {     QImage i = this->pixmap().toImage();     const int width = i.width();     const int height = i.height();     for (int y=0;y!=height;++y)     {       for (int x=0;x!=width;++x)       {         i.setPixel(           QPoint(x,y), //Position           QColor( //Color             (x+z+0)%256,             (y+z+0)%256,             (x+y+z)%256)           .rgb());       }     }     this->setPixmap(this->pixmap().fromImage(i));     ++z;   }   private:   int z; };   int main(int argc, char *argv[]) {   QApplication a(argc, argv);    //Create a scene to add the background sprite to   boost::shared_ptr<QGraphicsScene> scene(new QGraphicsScene);    //Create a background sprite to add to the scene   boost::shared_ptr<ChangingBackground> background(     new ChangingBackground(256,256));   scene->addItem(background.get());    //Create a view to display the scene   boost::shared_ptr<QGraphicsView> view(new QGraphicsView);   view->setScene(scene.get());    //Create a timer to call 'advance' on the scene and its sprite   boost::shared_ptr<QTimer> timer(new QTimer(scene.get()));   timer->connect(timer.get(), SIGNAL(timeout()), scene.get(), SLOT(advance()));   timer->start(20);    //Display the view   view->show();    //Move the view to the screen center   const QRect screen = QApplication::desktop()->screenGeometry();   view->move( screen.center() - view->rect().center() );    return a.exec(); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

