# Inheritance

It make sub class have a super class' derived properties and characteristics

1. Mode of Inheritance
   - Public mode
   - Protected mode
   - Private mode

  ```{.cpp}
  class A
  {
  public:
      int x;
  protected:
      int y;
  private:
      int z;
  };

  class B : public A // public mode
  {
      // x is public and is accesible from B class
      // y is protected and is accesible from B class
      // z is private and is not accessible from B class
  };

  class C : protected A // protected mode
  {
      // x is protected and is accesible from C class
      // y is protected and is accesible from C class
      // z is private and is not accessible from C class
  };

  class D : private A    // private mode is default
  {
      // x is private and is accesible from D class
      // y is private and is accesible from D class
      // z is private and is not accessible from D class
  };
  ```

2. Types of Inheritance
   - Single Inheritance
    a sub class inherits from only one class.

    ```{.cpp}
    class Base
    {
      public:
        Base()
        {
        }
        virtual ~Base()
        {
        }
      };

      class Derived : public Base {
      public:
        Derived()
        {
        }
        ~Derived()
        {
        }
    };
    ```

   - Multiple Inheritance
    a sub class inherits from more tahn one classes.

    ```{.cpp}
    class Base1
    {
      public:
        Base1()
        {
        }
        virtual ~Base1()
        {
        }
      };

      class Base2
    {
      public:
        Base2()
        {
        }
        virtual ~Base2()
        {
        }
      };

      class Derived : public Base1, public Base2 {
      public:
        Derived()
        {
        }
        ~Derived()
        {
        }
    };
    ```

3. Problem of multiple inheritance
  Problem of multiple inheritance induces ambiguity and complexity.
   - If super classes have same name function.

    ```{.cpp}
    class Base1
    {
      public:
        Base1()
        {
        }
        virtual ~Base1()
        {
        }
        void sameFunc()
        {
          cout << "Base1";
        }
      };

      class Base2
    {
      public:
        Base2()
        {
        }
        virtual ~Base2()
        {
        }
        void sameFunc()
        {
          cout << "Base2";
        }
      };

      class Derived : public Base1, public Base2 {
      public:
        Derived()
        {
        }
        ~Derived()
        {
        }
        void print()
        {
          sameFunc() // error
        }
    };
    ```

    It can be resolved by specifing which class' function called ex) Base1::sameFunc() but it makes relationships between Classes complex.

   - The diamond Problem

    ```{.cpp}
    class Parent
    {
      public:
        Parent()
        {
          cout << "Parent Class is constructed\n";
        }
        virtual ~Parent()
        {
        }
        void sameFunc()
        {
          cout << "Parent";
        }
      };

    class Middle1 : public Parent
    {
      public:
        Middle1()
        {
          cout << "Middle1 Class is constructed\n";
        }
        virtual ~Middle1()
        {
        }
        void sameFunc()
        {
          cout << "Middle1";
        }
    };

    class Middle2 : public Parent
    {
      public:
        Middle2()
        {
          cout << "Middle2 Class is constructed\n";
        }
        virtual ~Middle2()
        {
        }
        void sameFunc()
        {
          cout << "Middle2";
        }
      };

      class Derived : public Middle1, public Middle2 {
      public:
        Derived()
        {
          cout << "Derived Class is constructed\n";
        }
        ~Derived()
        {
        }
        void print()
        {
          sameFunc() // error
        }
    };
    int main()
    {
      Derived * derived = new Derived();
      /*
      Parent Class is constructed
      Middle1 Class is constructed
      Parent Class is constructed
      Middle2 Class is constructed
      Derived Class is constructed
      */
    }
    ```

    It results in calling Parent class' constructor twice. So derived object has two parent class' members.
    Above problem is resolved by virtual inheritance in Middle1 class and Middle2 class. but it makes relationships between Classes complex.
