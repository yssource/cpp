# ([C++](Cpp.md)) [operator==](CppOperatorEqual.md)

[operator==](CppOperatorEqual.md) is the [operator](CppOperator.md) to
determine if two [instances](CppInstance.md) are the same.

The following code uses [operator==](CppOperatorEqual.md) to determine
that one plus two is equal to three:

```c++
#include <iostream>

int main()
{
  if (1 + 2 == 3) std::cout << "One plus two is equal to three\n";
}
```

[operator==](CppOperatorEqual.md) is encapsulated by the
[functor](CppFunctor.md) [std::equal\_to](CppStdEqual_to.md).

## Overloading [operator==](CppOperatorEqual.md) for a user-defined type

Prefer making [operator==](CppOperatorEqual.md) a free function
[1,2].

-   [Download the Qt Creator project 'CppOperatorEqual' (zip)](CppOperatorEqual.zip)


```c++
#include <algorithm>
#include <functional>
#include <cassert>
#include <vector>

//Can even define both!
#define DEFINE_OPERATOR_EQUAL_AS_MEMBER_FUNCTION
#define DEFINE_OPERATOR_EQUAL_AS_FREE_FUNCTION

struct Test
{
  Test(const int x, const int y) : m_x(x), m_y(y) {}
  int GetX() const { return m_x; }
  int GetY() const { return m_y; }

  #ifdef DEFINE_OPERATOR_EQUAL_AS_MEMBER_FUNCTION
  bool operator==(const Test rhs)
  { return this->GetX() == rhs.GetX() && this->GetY() == rhs.GetY();
  }
  #endif

  private:
  int m_x;
  int m_y;
};


#ifdef DEFINE_OPERATOR_EQUAL_AS_FREE_FUNCTION
bool operator==(const Test& lhs, const Test rhs)
{
  return lhs.GetX() == rhs.GetX() && lhs.GetY() == rhs.GetY();
}
#endif

int main()
{
  std::vector<Test> v;
  v.push_back(Test(0,0));
  v.push_back(Test(1,1));
  v.push_back(Test(2,2));
  v.push_back(Test(0,0));
  assert(v[0] == v[3]); //Both ways work
  assert(std::count(v.begin(),v.end(),Test(0,0)) == 2); //Both ways work
}
```

## [References](CppReferences.md)

1.  [John Lakos](CppJohnLakos.md). Large-Scale C++ Software Design. 1996. ISBN: 0-201-63362-0. Paragraph 9.1.2, page 596: 'The conclusion is that operator== should always be a free function, regardless of what other functions are involved'
2.  [Herb Sutter](CppHerbSutter.md), [Andrei Alexandrescu](CppAndreiAlexandrescu.md). C++ coding standards: 101 rules, guidelines, and best practices. 2005. ISBN: 0-32-111358-6.

 

 

 

 

 

 

