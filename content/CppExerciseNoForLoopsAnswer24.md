# ([C++](Cpp.md)) [Answer of exercise \#9: No for-loops \#24](CppExerciseNoForLoopsAnswer24.md)

This is the answer of [Exercise \#9: No
for-loops](CppExerciseNoForLoops.md).

## Question \#24: [SumSecond](CppSumSecond.md)

Replace the **[for](CppFor.md)**-loop. You will need:

-   [boost::bind](CppStdBind.md)
-   [std::plus](CppStdPlus.md)

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` int SumSecond(const std::vector<std::pair<int,int> >& v) {   const int size = static_cast<int>(v.size());   int sum = 0;   for (int i=0; i!=size; ++i)   {     sum+=v[i].second;   }   return sum; }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## ![STL](PicStl.png) Answer using [STL](CppStl.md) only

You may [contact me](http://www.richelbilderbeek.nl/Contact.htm) if you have an [STL](CppStl.md)
solution...

## ![Boost](PicBoost.png) Answer using [Boost](CppBoost.md).Bind

Thanks to 'ofwolfandman':

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <functional> #include <numeric> #include <utility> #include <vector> #include <boost/bind.hpp>  int SumSecond(const std::vector<std::pair<int,int> >& v) {   return std::accumulate(     v.begin(),     v.end(),     static_cast<int>(0),     boost::bind(       std::plus<int>(),       _1,       boost::bind<int>(&std::pair<int,int>::second, _2)       )     ); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## ![Boost](PicBoost.png) Answer using [Boost](CppBoost.md).Lambda

Thanks to 'ofwolfandman':

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <functional> #include <numeric> #include <utility> #include <vector> #include <boost/lambda/lambda.hpp> #include <boost/lambda/bind.hpp>  int SumSecond(const std::vector<std::pair<int,int> >& v) {   return std::accumulate(     v.begin(),     v.end(),     static_cast<int>(0),     boost::lambda::_1     + boost::lambda::bind(       &std::pair<int, int>::second, boost::lambda::_2       )   ); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
