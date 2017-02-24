



 

 

 

 

 

([C++](Cpp.htm)) [operator()](CppOperatorFunctionCall.htm)
==========================================================

 

[operator()()](CppOperatorFunctionCall.htm) (pronounciation: 'function
call operator') is the [operator](CppOperator.htm) typically used by
[functors](CppFunctor.htm).

 

 

 

 

 

Example
-------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  struct Test {   //Definition of operator()   void operator()() const   {     std::cout << ".\n";   } };  int main() {   //Create a Test   Test t;    //Call operator()   t(); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Example: [GreaterThan](CppFunctorGreaterThan.htm)
-------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <functional> #include <numeric> #include <vector>  //From http://www.richelbilderbeek.nl/CppFunctorGreaterThan.htm struct GreaterThan : public std::binary_function<int,int,int> {   explicit GreaterThan(const int any_x = 0) : x(any_x) {}   int operator()(const int sum, const int y) const   {     return sum + (y <= x ? 0 : y);   }    private:   int x; };  const std::vector<int> CreateVector() {   std::vector<int> v;   v.push_back(-1);   v.push_back(0);   v.push_back(1);   v.push_back(2);   v.push_back(3);   v.push_back(4);   return v; }  int main() {   const std::vector<int> v = CreateVector();   assert(std::accumulate(v.begin(),v.end(),0,GreaterThan(5))==0);   assert(std::accumulate(v.begin(),v.end(),0,GreaterThan(4))==0);   assert(std::accumulate(v.begin(),v.end(),0,GreaterThan(3))==4);   assert(std::accumulate(v.begin(),v.end(),0,GreaterThan(2))==7);   assert(std::accumulate(v.begin(),v.end(),0,GreaterThan(1))==9);   assert(std::accumulate(v.begin(),v.end(),0,GreaterThan(0))==10); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Advice](CppAdvice.htm)
-----------------------

 

-   Use [operator()()](CppOperatorFunctionCall.htm) for call semantics,
    for subscripting, and for selection based on a multiple values \[1\]

 

 

 

 

 

[Reference](CppReferences.htm)
------------------------------

 

1.  [Bjarne Stroustrup](CppBjarneStroustrup.htm). The C++ Programming
    Language (4th edition). 2013. ISBN: 978-0-321-56384-2. Chapter 19.5.
    Advice. page 576: '\[2\] Use operator()() for call semantics, for
    subscripting, and for selection based on a multiple values'

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)