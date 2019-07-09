# Polymorphism

1. Compile time polymorphism
   - Function Overloading
     - It is that class has multiple same name functions but diffrent parameters.
     - Functions can be overloaded by change in number of arguments or/and change in type of arguments.

    ```{.cpp}
    #include<iostream>
    using namespace std;

    #ifndef PI
      #define PI 3.141592653589793f
    #endif

      class Sphere
      {
        public :

          void printVolume(float r)
          {
            cout << 4 / 3 * pow(radius, 3) * PI;
          }
           void printVolume(double r)
          {
            cout << 4 / 3 * pow(radius, 3) * PI;
          }
      };

      int main()
      {
        Sphere sphere;

        printVolume(3.0f);
        printVolume(4.0);

        return 0;
      }
    ```

   - Operator Overloading
    C++ Can overload operator ex) +

    ```{.cpp}
    #include<iostream>
    using namespace std;

    #ifndef PI
    #define PI 3.141592653589793f
    #endif

    class Sphere
    {
    private:
      float radius;
    public:
      Sphere(float r = 0)
      {
        radius = r;
      }
      Sphere operator + (Sphere &otherSphere)
      {
        Sphere res;
        res.radius = radius + otherSphere.radius;

        return res;
      }
      void printVolume()
      {
        cout << "Radius : " << pow(radius, 3) << "\n";
        cout << 4.0f / 3.0f * pow(radius, 3) * PI;
      }
    };

    int main()
    {
      Sphere *sphere1 = new Sphere(1.0f);
      Sphere *sphere2 = new Sphere(2.0f);
      Sphere sphere3 = *sphere1 + *sphere2;
      sphere3.printVolume();

      return 0;
    }
    ```

   - Casting operator overloading

    ```{.cpp}
    #include<iostream>
    using namespace std;
    class MyString
    {
    private :
      wchar_t string[20];
    public:
      MyString()
      {
        wcscpy_s(string, 20, L"Hello ");
        wchar_t* p = string;
      }
      virtual ~MyString()
      {
      }
      //This function is no need, if you use cating operator overloading
      wchar_t *getString()
      {
        return string;
      }
      //cating operator overloading
      operator wchar_t* ()
      {
        return string;
      }
    };

    int main()
    {
      MyString myString;
      /*
      not Using casting operator overloading
      wchar_t *str = myString.getString();
      wcout << str;
      */
      //cating operator overloading
      wcout << (wchar_t*)myString;
      return 0;
    }
    ```

2. Runtime polymorphism
   - Function overriding
    Derived class(sub) defines one of the member functions of the super class.
    Super class' functions overridden must be [virtual function](./virtual_function.md).
    It is diffent from function overloading that function overriding has same parameters.

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
        virtual void print ()
        {
          cout<< "base class\n";
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
        void print ()
        {
          cout<< "Derived class\n";
        }
    };
    int main()
    {
      Base *base;
      Derived d;
      base = &d;

      //virtual function, binded at runtime
      base->print();

      return 0;
    }
    ```
