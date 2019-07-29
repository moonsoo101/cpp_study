# STL

1. Algorithms
   1. Sorting
    Sorting function sorts a vector or array  in ascending or descending order.
    Internally this function is implemented as Quick-sort. The complexity of it is O(N*log(N)).
   2. reverse
    To reverse a vector.
   3. max_element
    To find the maximum element of a vector.
   4. min_element
    To find the minimum element of a vector.
   5. accmulate
    Does the summation of vector elements
   6. count
     To count the occurrences of x in vector.
   7. find
     Points to last address of vector ((name_of_vector).end()) if element exists in vector.
     Pints to element address of vector if element exists
   8. binary search
     To find element using binary search
   9. Array.erase(position)
      This erases selected element in vector and shifts and resizes the vector elements accordingly.

    ```{.cpp}
      #include <iostream>
      #include <algorithm>
      #include <vector>
      #include <numeric>

      using namespace std;

      int main()
      {
        int a[10] = { 1, 5, 3, 9, 6, 7, 3, 4, 2, 0 };
        int n = sizeof(a) / sizeof(a[0]);

        vector<int> vect(a, a + n);

        cout << "Vector is: ";
        for (int i = 0; i < n; i++)
            cout << vect[i] << " ";

        // Sorting the Vector in Ascending order
        sort(vect.begin(), vect.end());

        cout << "\nVector after sorting is: ";
        for (int i = 0; i < n; i++)
            cout << vect[i] << " ";

        // Reversing the Vector
        reverse(vect.begin(), vect.end());

        cout << "\nVector after reversing is: ";
        for (int i = 0; i < 6; i++)
            cout << vect[i] << " ";

        cout << "\nMaximum : ";
        cout << *max_element(vect.begin(), vect.end());

        cout << "\nMinimum : ";
        cout << *min_element(vect.begin(), vect.end());

        cout << "\nAccumulate: ";
        cout << accumulate(vect.begin(), vect.end(), 0);

        // Counts the occurrences of 20 from 1st to
      // last element
      cout << count(vect.begin(), vect.end(), 20);

      // find() returns iterator to last address if
      // element not present
      find(vect.begin(), vect.end(),5) != vect.end()? cout << "\nElement found" : cout << "\nElement not found";

      if (binary_search(a, a + 10, 6))
        cout << "\nElement found in the array";
      else
        cout << "\nElement not found in the array";

      // Delete second element of vector
      vect.erase(vect.begin()+1);

      return 0;

      }
    ```

2. Containers
3. Functions
4. Iterators