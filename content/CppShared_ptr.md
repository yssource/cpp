
 

 

 

 

 

([C++](Cpp.md)) shared\_ptr
============================

 

 

[shared\_ptr](CppShared_ptr.md) is a type of [smart
pointer](CppSmartPointer.md) that can be copied safely and cheap,
without copying the object [pointed](CppPointer.md) to. When the last
[shared\_ptr](CppShared_ptr.md) using an object goes out of
[scope](CppScope.md), it will **[delete](CppDelete.md)** the object
[pointed](CppPointer.md)to.

 

There are multiple types of [shared\_ptr](CppShared_ptr.md)s:

-   ![C++98](PicCpp98.png)![Boost](PicBoost.png)
    [boost::shared\_ptr](CppBoostShared_ptr.md)
-   ![C++98](PicCpp98.png)![STL](PicStl.png)
    [std::tr1::shared\_ptr](CppStdTr1Shared_ptr.md)
-   ![C++11](PicCpp11.png)![STL](PicStl.png)
    [std::shared\_ptr](CppStdShared_ptr.md)

 

 

 

 

 

External links
--------------

 

-   [GCC's page about
    std::shared\_ptr](http://gcc.gnu.org/onlinedocs/libstdc++/manual/shared_ptr.html)
-   [Boost's page about
    boost::shared\_ptr](http://www.boost.org/doc/libs/1_35_0/libs/smart_ptr/shared_ptr.md)

 

 

 

 

 

 

