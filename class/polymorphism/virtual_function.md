# Virtual Function

A virtual function a member function which is declared within a super class and is overriden by a sub class. It is called at Run-time.

1. Virtual functions cannot be static function and friend function of another class.
2. Virtual functions should be accessed using pointer of super class type.

- VTABLE
  Whether object is created or not, a static array of function pointer(VTABLE) which has the address of each virtual function contained in that class(derived virtual functions and overridden funtions).
- VPTR
  If object of that class is created then a virtual pointer(VPTR) is inserted as a data member of the class to point to VTABLE of that class. For each new object created, a new virtual pointer(VPTR) is inserted as a data member of that class.

  ```{.cpp}
  #include<iostream>
    using namespace std;
    class Base
    {
      public:
        Base()
        {
        }
        virtual ~Base()
        {
        }
        void fn1 () //this function isn't contained in Base's VTABLE
        {
          cout<< "base fn1\n";
        }
        virtual void fn2 ()
        {
          cout<< "base fn2\n";
        }
        virtual void fn4 () //this function is contained in Base's VTABL and Derived's VTABLE
        {
          cout<< "base fn4\n";
        }
        /*
          VTABLE of class Derived
          address of fn2 of Base class
          address of fn4 of Base class
        */
      };

      class Derived : public Base {
      public:
        Derived()
        {
        }
        ~Derived()
        {
        }
        void fn1 () //this function isn't contained in Derived's VTABLE
        {
          cout<< "derived fn1\n";
        }
        void fn2 () //this function is contained in Derived's VTABLE as Derived version
        {
          cout<< "derived fn2\n";
        }
        virtual void fn3 () //this function isn't contained in Derived's VTABLE
        {
          cout<< "Derived fn3\n";
        }
        void fn4 (int a) //this function isn't contained in Derived's VTABLE
        {
          cout<< "Derived fn4\n";
        }
        /*
          VTABLE of class Derived
          address of fn2 of Derived class
          address of fn4 of Base class
        */
    };
    int main()
    {
      Base *base;
      Derived d;
      base = &d; // VPTR points to VTABLE of Derived class


      //virtual function, binded at runtime
      base->fn1(); // this function is non-virtual, That's why early binding(compile-tile) occurs
      base->fn2(); // late binding(run-time)
      /*
      It occurs compile error.
      base->fn3();
      */
      base->fn4(); // late binding(run-time)

      /*
      RESULT :
      base fn1
      derived fn2
      base fn4
      */

      return 0;
    }
    ```
