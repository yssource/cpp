
 

 

 

 

 

([C++](Cpp.md)) [std::setbase](CppStdSetbase.md)
===============================================

 

[std::setbase](CppStdSetbase.md) is a [stream](CppStream.md) manipulator
to change the output of numbers to the octal, decimal or hexadecimal
number system.

 

-   [Download the Qt Creator project 'CppSetbase' (zip)](CppSetbase.zip)

 

 

 

 

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <iomanip> int main() {   for (int i=0; i!=20; ++i)   {     std::cout       << std::setbase(10) << i << "(dec) "       << std::setbase(8)  << i << "(oct) "       << std::setbase(16) << i << "(hex)"       << '\n';   } }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Screen output:

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` 0(dec) 0(oct) 0(hex) 1(dec) 1(oct) 1(hex) 2(dec) 2(oct) 2(hex) 3(dec) 3(oct) 3(hex) 4(dec) 4(oct) 4(hex) 5(dec) 5(oct) 5(hex) 6(dec) 6(oct) 6(hex) 7(dec) 7(oct) 7(hex) 8(dec) 10(oct) 8(hex) 9(dec) 11(oct) 9(hex) 10(dec) 12(oct) a(hex) 11(dec) 13(oct) b(hex) 12(dec) 14(oct) c(hex) 13(dec) 15(oct) d(hex) 14(dec) 16(oct) e(hex) 15(dec) 17(oct) f(hex) 16(dec) 20(oct) 10(hex) 17(dec) 21(oct) 11(hex) 18(dec) 22(oct) 12(hex) 19(dec) 23(oct) 13(hex)`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

