



 

 

 

 

 

([C++](Cpp.htm)) [PaperRockScissorsSimulation](CppPaperRockScissorsSimulation.htm)
==================================================================================

 

Technical facts
---------------

 

 

 

 

 

 

./CppPaperRockScissorsSimulation/CppPaperRockScissorsSimulation.pri
-------------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppPaperRockScissorsSimulation  SOURCES += \     ../../Classes/CppPaperRockScissorsSimulation/paperrockscissorssimulation.cpp  HEADERS  += \     ../../Classes/CppPaperRockScissorsSimulation/paperrockscissorssimulation.h  OTHER_FILES += \     ../../Classes/CppPaperRockScissorsSimulation/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppPaperRockScissorsSimulation/paperrockscissorssimulation.h
--------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef PAPERROCKSCISSORSSIMULATION_H #define PAPERROCKSCISSORSSIMULATION_H  #include <random> #include <vector> #include "paperrockscissors.h"  namespace ribi { namespace prs {  struct PaperRockScissorsSimulation {   using CellType = PaperRockScissors;    enum class Initialization   {     random,     vertical_bands   };    PaperRockScissorsSimulation(     const int width,     const int height,     const Initialization initialization,     const int rng_seed   );    ///Y-X ordered grid   const std::vector<std::vector<CellType>>& GetGrid() const noexcept { return m_grid; }   Initialization GetInitialization() const noexcept { return m_initialization; }   void Next();   void SetInitialization(const Initialization initialization) noexcept;    private:    std::vector<std::vector<CellType>> m_grid;   Initialization m_initialization;   int m_rng_seed;   std::mt19937 m_rng; };  } //~namespace prs { } //~namespace ribi {  #endif // PAPERROCKSCISSORSSIMULATION_H`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppPaperRockScissorsSimulation/paperrockscissorssimulation.cpp
----------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "paperrockscissorssimulation.h"  #include <array> #include <cassert> #include <algorithm> #include <cstdlib>   ribi::prs::PaperRockScissorsSimulation::PaperRockScissorsSimulation(   const int width,   const int height,   const Initialization initialization,   const int rng_seed )   : m_grid{       std::vector<std::vector<CellType>>(         height,         std::vector<CellType>(width,CellType::paper)       )     },   m_initialization{initialization},   m_rng_seed{rng_seed},   m_rng(rng_seed) {   SetInitialization(m_initialization); }  void ribi::prs::PaperRockScissorsSimulation::Next() {   static std::uniform_int_distribution<int> d(0,3); //Inclusive    std::vector<std::vector<CellType>> next(m_grid);   const int height{static_cast<int>(m_grid.size())};   const int width{static_cast<int>(m_grid[0].size())};   for (int y=0; y!=height; ++y)   {     for (int x=0; x!=width; ++x)     {       int dx{0};       int dy{0};        switch (d(m_rng))       {         case 0: --dy; break;         case 1: ++dx; break;         case 2: ++dy; break;         case 3: --dx; break;         default: assert(!"Should not get here");       }       CellType& here{m_grid[y][x]};       const CellType& neighbour{m_grid[(y+dy+height)%height][(x+dx+width)%width]};       next[y][x] = DoesBeat(neighbour,here) ? neighbour : here;     }   }   std::swap(m_grid,next); }  void ribi::prs::PaperRockScissorsSimulation::SetInitialization(const Initialization initialization) noexcept {   m_initialization = initialization;    //Initialize the grid   const int height{static_cast<int>(m_grid.size())};   assert(!m_grid.empty());   const int width{static_cast<int>(m_grid[0].size())};   for (int y=0; y!=height; ++y)   {     for (int x=0; x!=width; ++x)     {       CellType& celltype = m_grid[y][x];       switch(m_initialization)       {         case Initialization::random:         {           static std::uniform_int_distribution<int> d(0,2); //Inclusive           switch (d(m_rng))           {             case 0: celltype = CellType::paper; break;             case 1: celltype = CellType::rock; break;             case 2: celltype = CellType::scissors; break;             default: assert(!"Should not get here");           }         }           break;         case Initialization::vertical_bands:           {             switch ((y / (height / 15)) % 3)             {               case 0: celltype = CellType::paper; break;               case 1: celltype = CellType::rock; break;               case 2: celltype = CellType::scissors; break;             }           }         break;       }     }   } }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)