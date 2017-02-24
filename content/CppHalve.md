



 

 

 

 

 

([C++](Cpp.htm)) [Halve](CppHalve.htm)
======================================

 

 

[Halve](CppHalve.htm) is a [container](CppContainer.htm) [code
snippet](CppCodeSnippets.htm) to replace all values in a
[container](CppContainer.htm) by their halves (that is: x/2.0).

 

There are multiple ways to perform [Halve](CppHalve.htm):

-   The general algorithm way (best)
-   The algorithm way on a std::vector&lt;double&gt; (intermediate)
-   The for-loop way on a std::vector&lt;double&gt; (worst)

 

 

 

 

 

The general algorithm way
-------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <numeric>  //From http://www.richelbilderbeek.nl/CppHalve.htm template <class Container> void Halve(Container& c) {   std::transform(c.begin(),c.end(),c.begin(),     std::bind2nd(std::divides<Container::value_type>(),2.0));     }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

The algorithm way on a [std::vector&lt;](CppVector.htm)[double](CppDouble.htm)&gt;
----------------------------------------------------------------------------------

 

This way is used as an answer in [Exercise \#9: No
for-loops](CppExerciseNoForLoops.htm).

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector> #include <algorithm> #include <numeric>  //From http://www.richelbilderbeek.nl/CppHalve.htm void Halve(std::vector<double>& v) {   std::transform(v.begin(),v.end(),v.begin(),     std::bind2nd(std::divides<double>(),2.0));     }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

The[for](CppFor.htm)-loop way on a [std::vector&lt;](CppVector.htm)[double](CppDouble.htm)&gt;
----------------------------------------------------------------------------------------------

 

Prefer [algorithms](CppAlgorithm.htm) over loops \[1,2\].

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector>  //From http://www.richelbilderbeek.nl/CppHalve.htm void Halve(std::vector<double>& v) {   const int sz = v.size();   for (int i=0; i!=sz; ++i)   {     v[i]/=2.0;   } }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[References](CppReferences.htm)
-------------------------------

 

1.  [Bjarne Stroustrup](CppBjarneStroustrup.htm). The C++ Programming
    Language (3rd edition). ISBN: 0-201-88954-4. Chapter 18.12.1 :
    'Prefer algorithms over loops'
2.  [Herb Sutter](CppHerbSutter.htm) and [Andrei
    Alexandrescu](CppAndreiAlexandrescu.htm). C++ coding standards: 101
    rules, guidelines, and best practices. ISBN: 0-32-111358-6. Chapter
    84: 'Prefer algorithm calls to handwritten loops.'

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)