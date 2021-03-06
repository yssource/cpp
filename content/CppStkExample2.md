
 

 

 

 

 

([C++](Cpp.md)) [StkExample2](CppStkExample2.md)
==================================================

 

![C++11](PicCpp11.png)![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[STK example 2: random beeps](CppStkExample2.md) is an
[STK](CppStk.md) example that generates random beeps infinitely (note:
you cannot stop the program). The code was modified from
<https://ccrma.stanford.edu/software/stk/crealtime.html>.

 

Note that the original copy-pasted code resulted in multiple [compile
warnings](CppCompileWarning.md) and that the [library](CppLibrary.md)
style, design and example code looks different from the experts'
recommendations

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppStkExample2/CppStkExample2.pro
----------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `  include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }   # Install STK by: # sudo apt-get install libstk0-dev include(../../Libraries/Stk.pri) #Or use the code below # INCLUDEPATH += /usr/include/stk # LIBS += -L/usr/lib -lstk -lrtaudio  SOURCES += main.cpp`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStkExample2/main.cpp
-------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `  //From http://www.richelbilderbeek.nl/CppStk.htm //Modified from crtsine.cpp STK tutorial program #include <boost/static_assert.hpp> #include <boost/timer.hpp>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-variable" #include "SineWave.h" #include "RtAudio.h" #pragma GCC diagnostic pop  // This tick() function handles sample computation only. It will be // called automatically when the system needs a new buffer of audio // samples. int tick(   void *outputBuffer, void * /*inputBuffer*/,   unsigned int nBufferFrames,   double /*streamTime*/, RtAudioStreamStatus /*status*/,   void *dataPointer) {   stk::SineWave * const sine = (stk::SineWave *) dataPointer;   stk::StkFloat * samples = (stk::StkFloat *) outputBuffer;    for ( unsigned int i=0; i!=nBufferFrames; ++i )     *samples++ = sine->tick();   return 0; }   int main() {   // Set the global sample rate before creating class instances.   stk::Stk::setSampleRate( 44100.0 );    // Setup the RtAudio stream.   RtAudio dac;   RtAudio::StreamParameters parameters;   parameters.deviceId = dac.getDefaultOutputDevice();   parameters.nChannels = 1;   BOOST_STATIC_ASSERT(sizeof(stk::StkFloat) == 8);   unsigned int bufferFrames = stk::RT_BUFFER_SIZE;    while (1)   {     //Choose a random beep frequency     stk::SineWave sine;     dac.openStream(       &parameters, NULL,       RTAUDIO_FLOAT64,       (unsigned int)stk::Stk::sampleRate(),       &bufferFrames, &tick,       (void *)&sine );     sine.setFrequency(100.0       + static_cast<double>(std::rand()%1000));     dac.startStream();     //Let it beep for 0.2 seconds     boost::timer t;     while (t.elapsed() < 0.2 ) {}     //Prepare for next beep     dac.closeStream();   } }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

