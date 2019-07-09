# Constructor and Destructor

## Constructor

1. Constructor must have same name as the class' name
2. Constructor doesn’t have return type
3. A constructor is automatically called when an object is created
4. If you do not specify a constructor, C++ compiler generates a default constructor(no parameters and empty body)

- default initializer
  - A temporary object would be created which will be provided to the assignment operator. The temporary object will be destroyed at the end of the assignment statement.

```{.cpp}
#include<iostream>
using namespace std;

class A
{
  private:
    int number;
    int b;
  public:
    // It can initialize const member
    A(int number, int b)
    {
      this->number = number;
      this->b = b;
    }
    void printMembers()
    {
      cout << "number : " << number << " b : " << b << "\n";
    }
  };

  int main() {

    A * a = new A(3, 4);

    a->printMembers();
  return 0;
}
```

- Initializer List
  - Unlike default initializer, the members are created and initialized only once, that's why creation of temporary object can be avoided.
  - It can initialize const member.

```{.cpp}
#include<iostream>
using namespace std;

class A
{
  private:
    const int NUMBER;
    int b;
  public:
    // It can initialize const member
    A(int number, int b)
      : NUMBER(number), b(b)
    {

    }
    void printMembers()
    {
      cout << "NUMBER : " << NUMBER << " b : " << b << "\n";
    }
  };

  int main() {

    A * a = new A(3, 4);

    a->printMembers();
  return 0;
}
```

- Constructor Delegation
  - It is a constructor that can call another constructor in same class

```{.cpp}
#include <iostream>
using namespace std;
class Base {
    int x, y, z;

public:
    Base()
    {
        x = 0;
        y = 0;
        z = 0;
    }

    // Constructor Delegation
    Base(int z) : Base()
    {
        /*
        this->x = 0;
        this->y = 0;
        */
        this->z = z;
    }

    void printMember()
    {
        cout << x << '\n'
             << y << '\n'
             << z;
    }
};
int main()
{
    Base * base = new Base(5);
    base.printMember();

    return 0;
}
```

## Destructor

1. It destructs or deletes an object.
2. It has same name as the class' name preceded by a tilde (~)
3. It is called automatically when the object goes out of scope
   - the function ends
   - the program ends
   - a block containing local variables ends
   - a delete operator is called
4. It doesn't return and doesn't have arguments.

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
  Sphere(float radius)
  {
    this->radius = radius;
  }
  ~Sphere()
  {
    cout << "destructor called, Radius : " << radius << "\n";
  }
  float getSphereVolume()
  {
    return 4.0f / 3.0f * pow(radius, 3) * PI;
  }
};

int main()
{
  Sphere * sphere1;
  Sphere * sphere2;

  sphere1 = new Sphere(1.0f);
  sphere2 = new Sphere(0.5f);
  cout << "Volume1 : " << sphere1->getSphereVolume() << "\n";
  cout << "Volume2 : " << sphere2->getSphereVolume() << "\n";
  delete sphere1;

  return 0;
}
```

5. Virtual Destructor

- Deleting a sub(derived) class object pointing a super class that has a non-virtual destructor doesn't call sub(derived) class' constructor.

```{.cpp}
#include<iostream>

using namespace std;

class Base {
public:
  Base()
  {
    cout << "Base class is constructed. \n";
  }
  ~Base()
  {
    cout << "Base class is destructed.\n";
  }
};

class Derived : public Base {
public:
  Derived()
  {
    cout << "Derived class is constructed. \n";
  }
  ~Derived()
  {
    cout << "Derived class is destructed.\n";
  }
};

int main(void)
{
  Base * d = new Derived();
  //Derived class' destructor isn't called
  delete d;

  return 0;
}
```

- If you make Super class' constructor virtual, It can be called When sub class destructs.

```{.cpp}
#include<iostream>

using namespace std;

class Base {
public:
  Base()
  {
    cout << "Base class is constructed.\n";
  }
  virtual ~Base()
  {
    cout << "Base class is destructed.\n";
  }
};

class Derived : public Base {
public:
  Derived()
  {
    cout << "Derived class is constructed. \n";
  }
  ~Derived()
  {
    cout << "Derived class is destructed.\n";
  }
};

int main(void)
{
  Base * d = new Derived();
  //Derived class' destructor will be called
  delete d;

  return 0;
}
```
