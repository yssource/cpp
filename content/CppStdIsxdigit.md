
 

 

 

 

 

([C++](Cpp.md)) [std::isxdigit](CppIsxdigit.md)
=================================================

 

[std::isxdigit](CppIsxdigit.md) is an [STL](CppStl.md)
[function](CppFunction.md) to test of a character is a hexadecimal
digit.

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <string>  int main() {   const std::string s = "1a";    //'a' is no decimal digit   assert( std::isdigit(s[0]));   assert(!std::isdigit(s[1]));    //'a' is a hexadecimal digit   assert( std::isxdigit(s[0]));   assert( std::isxdigit(s[1])); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

