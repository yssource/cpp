



 

 

 

 

 

([C++](Cpp.htm)) [std::length\_error](CppLength_error.htm)
==========================================================

 

[std::length\_error](CppLength_error.htm) (a [derived
class](CppDerivedClass.htm) from
[std::runtime\_error](CppRuntime_error.htm)) is [thrown](CppThrow.htm)
when a too big [std::string](CppString.htm) is created.

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <stdexcept> #include <string>  int main() {   std::string s;   try   {     s.resize(s.max_size()+1);   }   catch (std::length_error& e)   {     std::cout << e.what();   } }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)