
 

 

 

 

 

([C++](Cpp.md)) [operator\^](CppOperatorBitwiseXor.md)
========================================================

 

[operator\^](CppOperatorBitwiseXor.md) (pronounced as 'bitwise xor
operator') is an [operator](CppOperator.md) to perform a xor and
subsequently assign the result.

 

In the example below a '0011' is performed xor on with '0101' yielding
'0110', which equals the decimal value of 6.

 

  -------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert>  int main() {   const int i = 3;     //0011   const int j = 5;     //0101   const int k = i ^ j; //0110   assert(i==6); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

