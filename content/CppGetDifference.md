
 

 

 

 

 

([C++](Cpp.md)) [GetDifference](CppGetDifference.md)
======================================================

 

[GetDifference](CppGetDifference.md) is a [math](CppMath.md) [code
snippet](CppCodeSnippets.md) to get get a difference
[std::vector](CppStdVector.md) from [std::vectors](CppStdVector.md).

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <vector>  //From http://www.richelbilderbeek.nl/CppGetDifference.htm template <typename T> const std::vector<T> GetDifference(   const std::vector<T>& a,   const std::vector<T>& b) {   assert(a.size()==b.size());   std::vector<T> v(a);   const std::size_t sz = v.size();   for (std::size_t i = 0; i!=sz; ++i)   {     v[i]-=b[i];   }   return v; }  `
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

