c++ notes
=========

1. Why should use member initialization list?
---------------------------------------------

For POD class members, it makes no difference.

For class members which are classes, then it avoids an unnecessary 
call to a default constructor.

Furthermore, if a class doesn't have a default constructor, 
or you have a const member variable, you must use an initializer list:


