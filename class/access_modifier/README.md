# Access Modifier

In c++, default access modifier is private

## public

- All the class members declared under public will be available to everyone. The data members and member functions declared public can be accessed by other classes too. The public members of a class can be accessed from anywhere in the program using the direct member access operator (.) with the object of that class

```{.cpp}
#include<iostream>
using namespace std;

#ifndef PI
  #define PI 3.141592653589793f
#endif

  class Sphere
  {
    public :
      float radius;
      float getSphereVolume()
      {
        return 4.0f / 3.0f * pow(radius, 3) * PI;
      }
  };

  int main()
  {
    Sphere sphere;

    //can be accessed outside class
    sphere.radius = 1.0f;

    cout << "Radius : " << sphere.radius << "\n";
    cout << "Volue : " << sphere.getSphereVolume() << "\n";

    return 0;
  }
```

## private

- The class members declared as private can be accessed only by the functions inside the class. They are not allowed to be accessed directly by any object or function outside the class. Only the member functions or the friend functions are allowed to access the private data members of a class.

```{.cpp}
#include<iostream>
using namespace std;

#ifndef PI
  #define PI 3.141592653589793f
#endif

  class Sphere
  {
    private :
      float radius;
    public :
      void setRadius(float radius)
      {
        this->radius = radius;
      }
      float getRadius()
      {
        return radius;
      }
      float getSphereVolume()
      {
        return 4.0f / 3.0f * pow(radius, 3) * PI;
      }
  };

  int main()
  {
    Sphere sphere;

    //this line will throw a compile time error
    //sphere.radius = 1.0f;
    sphere.setRadius(1.0f);

    cout << "Radius : " << sphere.getRadius() << "\n";
    cout << "Volue : " << sphere.getSphereVolume() << "\n";

    return 0;
  }
```

- For information Hiding, It can be accessed by limited method can prevent your program from generating a logical error.  
The class member radius must be positive number. However, because it is declared as public, It can throw a logical error as below code.

```{.cpp}
#include<iostream>
using namespace std;

#ifndef PI
  #define PI 3.141592653589793f
#endif

  class Sphere
  {
    public :
      float radius;
      float getSphereVolume()
      {
        return 4.0f / 3.0f * pow(radius, 3) * PI;
      }
  };

  int main()
  {
    Sphere sphere;

    //can be accessed outside class, radius must be positive number
    sphere.radius = -1.0f;

    cout << "Radius : " << sphere.radius << "\n";
    cout << "Volue : " << sphere.getSphereVolume() << "\n";

    return 0;
  }
```

- If the class memeber radius is declared as private, It can prevent your program from generating a logical error

```{.cpp}
#include<iostream>
using namespace std;

#ifndef PI
  #define PI 3.141592653589793f
#endif

  class Sphere
  {
    private :
      float radius;
    public :
      void setRadius(float radius)
      {
        if ( radius <= 0 )
          throw -1;

        this->radius = radius;
      }
      float getRadius()
      {
        return radius;
      }
      float getSphereVolume()
      {
        return 4.0f / 3.0f * pow(radius, 3) * PI;
      }
  };

  int main()
  {
    Sphere sphere;

    try
    {
      sphere.setRadius(0);

      cout << "Radius : " << sphere.getRadius() << "\n";
      cout << "Volue : " << sphere.getSphereVolume() << "\n";
    }
    catch (const int errorCode)
    {
      cout  << "error code : " << errorCode;
    }

    return 0;
  }
```

## protected

- Protected access modifier is similar to that of private access modifiers
  - the class member declared as Protected are inaccessible outside the class
- Differrence
  - the class member declared as Protected can be accessed by any subclass(derived class) of that class.

```{.cpp}
  #include<iostream>
  using namespace std;

  class Parent
  {
  protected:
    int id;

  };

  // sub class(derived class)
  class Child : public Parent
  {
  public:
    void setId(int id)
    {
      this->id = id;

    }
    int getId()
    {
      return id;
    }
  };

  int main()
  {
    Child child;

    child.setId(10);
    cout << "ID : " << child.getId;
    return 0;
  }
```
