
 

 

 

 

 

([C++](Cpp.md) ) [std::for\_each](CppStdFor_each.md)
===================================================

 

[Algorithm](CppAlgorithm.md) to perform a non-modifying
[function](CppFunction.md) on the elements of a sequence (on a
[std::vector](CppStdVector.md), for example). Use
[std::transform](CppStdTransform.md) to perform modifying
[functions](CppFunction.md) on the elements of a sequence.

 

Prefer [algorithms](CppAlgorithm.md) over hand-written loops \[1-3\].
View [Exercise \#9: No for-loops](CppExerciseNoForLoops.md) to learn
how to remove hand-written loops .

 

Note: [std::for\_each](CppStdFor_each.md) is supposed to be non-modifying
\[1\], but I use it for modifying my sequences anyway.

 

There are two kinds of examples below. The first uses
[std::for\_each](CppStdFor_each.md) combined with simple
[functions](CppFunction.md).

 

The second piece of code shows the use of [functors](CppFunctor.md) for
more advanced functionality. It is advised to use the latter \[3\], but
I will show the first as an example. There are also [STL](CppStl.md)
[functors](CppFunctor.md).

 

 

 

 

 

Example: Use of plain [functions](CppFunction.md)
--------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorith> #include <iostream> #include <vector>   void SetToOne(int& i) {   i = 1; }   void MultiplyByTwo(int& i) {   i*=2; }   void SetToRandom(int& i) {   i = std::rand() % 10; }   void CoutVector(const std::vector<int>& myVector) {   const int size = static_cast<int>(myVector.size());   for (int i=0; i!=size; ++i)   {     std::cout << i << " : " << myVector[i] << std::endl;   } }  int main() {   const int size = 5;   std::vector<int> myVector(size);   std::for_each(myVector.begin(),myVector.end(), SetToOne);   CoutVector(myVector);   std::for_each(myVector.begin(),myVector.end(), MultiplyByTwo);   CoutVector(myVector);   std::for_each(myVector.begin(),myVector.end(), SetToRandom);   CoutVector(myVector);   std::for_each(myVector.begin(),myVector.end(), MultiplyByTwo);   CoutVector(myVector); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Example: Use of non-[STL](CppStl.md) [functors](CppFunctor.md)
----------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorith> #include <iostream> #include <vector>   struct MyInitializer {   MyInitializer() : index(0) {}   template<class T>   void operator () (T & a)   {     a = index;     ++index;   } private:   int index; };   struct MyIndexCout {   MyIndexCout() : index(0) {}   template<class T>   void operator () (const T & a)   {     std::cout << index << " : " << a << std::endl;     ++index;   } private:   int index; };   struct MySquarer {   template<class T> void operator () (T & a)   {     a*=a;   } };   int main() {   const int size = 10;   std::vector<int> myVector(size);   std::for_each(myVector.begin(), myVector.end(), MyInitializer());   std::for_each(myVector.begin(), myVector.end(), MyIndexCout());   std::cout << "-----------" << std::endl;   std::for_each(myVector.begin(), myVector.end(), MySquarer());   std::for_each(myVector.begin(), myVector.end(), MyIndexCout()); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[References](CppReferences.md)
-------------------------------

 

1.  Bjarne Stroustrup. The C++ Programming Language (3rd edition).
    ISBN: 0-201-88954-4. Chapter 18.12.1 : 'Prefer algorithms over
    loops'
2.  Herb Sutter and Andrei Alexandrescu. C++ coding standards: 101
    rules, guidelines, and best practices. ISBN: 0-32-111358-6. Chapter
    84: 'Prefer algorithm calls to handwritten loops.'
3.  Herb Sutter and Andrei Alexandrescu. C++ coding standards: 101
    rules, guidelines, and best practices. ISBN: 0-32-111358-6. Chapter
    88: 'Prefer function objects over functions as algorithm and
    comparer arguments.'

 

 

 

 

 

 

