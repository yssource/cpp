
 

 

 

 

 

([C++](Cpp.md)) [Exceptional C++: item 20](CppExceptionalCpp20.md)
====================================================================

 

[Exceptional C++: item 20](CppExceptionalCpp20.md) contains the code
from [Exceptional C++](CppExceptionalCpp.md) item 20.

 

-   [Download the Qt Creator project
    'CppExceptionalCpp20' (zip)](CppExceptionalCpp20.zip)

 

 

 

 

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` ///Completed from /// * Herb Sutter. Exceptional C++. ISBN: 0-201-61562-2. Item 20 #include <iostream> using namespace std;  class Complex { public:   Complex( double real, double imaginary = 0 )     : _real(real), _imaginary(imaginary) {};    void operator+ ( Complex other ) {     _real = _real + other._real;     _imaginary = _imaginary + other._imaginary;   }    void operator<<( ostream os ) {     os << "(" << _real << "," << _imaginary << ")";   }    Complex operator++() {     ++_real;     return *this;   }    Complex operator++( int ) {     Complex temp = *this;     ++_real;     return temp;   }  private:   double _real, _imaginary; };  int main() {  }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[References](CppReferences.md)
-------------------------------

 

1.  [Herb Sutter](CppHerbSutter.md). [Exceptional
    C++](CppExceptionalCpp.md). ISBN: 0-201-61562-2.

 

 

 

 

 

 

