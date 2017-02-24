



 

 

 

 

 

([C++](Cpp.htm)) [Answer of exercise \#9: No for-loops \#22](CppExerciseNoForLoopsAnswer22.htm)
===============================================================================================

 

This is the answer of [Exercise \#9: No
for-loops](CppExerciseNoForLoops.htm).

 

 

 

 

 

Question \#22: [CopySecond](CppCopySecond.htm)
----------------------------------------------

 

Replace the **[for](CppFor.htm)**-loop. You will need:

-   [boost::bind](CppBind.htm)

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector>  ///CopySecond copies the second std::pair elements from a std::vector of std::pairs //From http://www.richelbilderbeek.nl/CppCopySecond.htm template <class T, class U> const std::vector<U> CopySecond(const std::vector<std::pair<T,U> >& v) {   std::vector<U> w;   const int size = static_cast<int>(v.size());   for (int i=0; i!=size; ++i)   {     w.push_back(v[i].second);   }   return w; }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

-   [View the answer of this
    exercise](CppExerciseNoForLoopsAnswer22.htm)

 

 

 

 

 

Answer
------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <vector> #include <boost/lambda/bind.hpp> #include <boost/lambda/lambda.hpp>  ///CopySecond copies the second std::pair elements from a std::vector of std::pairs //From http://www.richelbilderbeek.nl/CppCopySecond.htm template <class T, class U> const std::vector<U> CopySecond(const std::vector<std::pair<T,U> >& v) {   std::vector<U> w;   std::transform(     v.begin(),     v.end(),     std::back_inserter(w),     boost::lambda::bind(&std::pair<T,U>::second, boost::lambda::_1)     );   return w; }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)