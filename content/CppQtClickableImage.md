
 

 

 

 

 

([C++](Cpp.md)) [QtClickableImage](CppQtClickableImage.md)
============================================================

 

Technical facts
---------------

 

 

 

 

 

 

./CppQtClickableImage/CppQtClickableImage.pri
---------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppQtClickableImage  SOURCES += \     ../../Classes/CppQtClickableImage/qtclickableimage.cpp  HEADERS  += \     ../../Classes/CppQtClickableImage/qtclickableimage.h  OTHER_FILES += \     ../../Classes/CppQtClickableImage/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtClickableImage/qtclickableimage.h
----------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTIMAGE_H #define QTIMAGE_H  #include <vector> #include <utility> #include <QRect> #include <QLabel>  struct QMouseEvent;  class QtImage : public QLabel {     Q_OBJECT public:     explicit QtImage(QWidget *parent = 0);     void AddClickableRegion(const QRect& region,const std::function<void()>& function_to_do);     void mouseMoveEvent(QMouseEvent * e);     void mousePressEvent(QMouseEvent * e);  protected:  private:   std::vector<std::pair<QRect,std::function<void()>>> m_v;  signals:  public slots:    };  #endif // QTIMAGE_H`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtClickableImage/qtclickableimage.cpp
------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "qtimage.h"  #include <iostream> #include <QMouseEvent>  QtImage::QtImage(QWidget *parent)   : QLabel(parent),     m_v{} {   this->setMouseTracking(true); }  void QtImage::AddClickableRegion(const QRect& region,const std::function<void()>& function_to_do) {   m_v.push_back(std::make_pair(region,function_to_do)); }  void QtImage::mouseMoveEvent(QMouseEvent *e) {   bool is_arrow = true;   //std::clog << e->pos().x() << ',' << e->pos().y() << '\n';   for (const auto p: m_v)   {     if (p.first.contains(e->pos()))     {       is_arrow = false;       //std::clog << e->pos().x() << ',' << e->pos().y() << '\n';     }   }   this->setCursor(QCursor(is_arrow ? Qt::ArrowCursor : Qt::PointingHandCursor)); }  void QtImage::mousePressEvent(QMouseEvent *e) {   //std::clog << e->pos().x() << ',' << e->pos().y() << '\n';   for (const auto p: m_v)   {     if (p.first.contains(e->pos()))     {       const auto f = p.second;       f();     }   } }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

