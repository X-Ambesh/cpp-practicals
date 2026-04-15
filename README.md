# cpp-practicals

### 1. Write a program to compute the sum of the first n terms of the following series: The
number of terms n is to be taken from the user through the command line. If the
command line argument is not found then prompt the user to enter the value of n.


```cpp
#include <iostream>
#include <cstdlib>  

using namespace std;

int main(int argc, char* argv[]) {
    int n;
    int sum = 0;

    if (argc > 1) {
        n = atoi(argv[1]);  
    } else {
        cout << "Enter the value of n: ";
        cin >> n;
    }

    for (int i = 1; i <= n; i++) {
        sum += i;
    }

    cout << "Sum of first " << n << " terms = " << sum << endl;

    return 0;
}
```

### 2. Write a program to remove the duplicates from an array.

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[100], n;

    cout << "Enter number of elements: ";
    cin >> n;

    cout << "Enter elements:\n";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] == arr[j]) {
                
                for (int k = j; k < n - 1; k++) {
                    arr[k] = arr[k + 1];
                }
                n--;
                j--;      
            }
        }
    }

    cout << "Array after removing duplicates:\n";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

### 3. Write a program that prints a table indicating the number of occurrences of each alphabet
in the text entered as command line arguments.


```cpp
#include <iostream>
#include <cctype>   
using namespace std;

int main(int argc, char* argv[]) {
    int count[26] = {0};  

    if (argc < 2) {
        cout << "Please provide text as command line arguments.\n";
        return 1;
    }

    for (int i = 1; i < argc; i++) {
        for (int j = 0; argv[i][j] != '\0'; j++) {
            char ch = argv[i][j];

            if (isalpha(ch)) {
                ch = tolower(ch);              
                count[ch - 'a']++;
            }
        }
    }

    cout << "Alphabet occurrence table:\n";
    for (int i = 0; i < 26; i++) {
        if (count[i] > 0) {
            cout << char('A' + i) << " : " << count[i] << endl;
        }
    }

    return 0;
}
```

###  4. Write a menu driven program to perform string manipulation (without using inbuilt string
functions):
a. Show address of each character in string
b. Concatenate two strings.
c. Compare two strings
d. Calculate length of the string (use pointers)
e. Convert all lowercase characters to uppercase
f. Reverse the string
g. Insert a string in another string at a user specified position



```cpp
#include <iostream>
using namespace std;

int length(char *s) {
    int len = 0;
    while (*(s + len) != '\0') len++;
    return len;
}

int compare(char *a, char *b) {
    int i = 0;
    while (a[i] != '\0' && b[i] != '\0') {
        if (a[i] != b[i]) return a[i] - b[i];
        i++;
    }
    return a[i] - b[i];
}

void concatenate(char *a, char *b) {
    int i = 0, j = 0;
    while (a[i] != '\0') i++;
    while (b[j] != '\0') {
        a[i] = b[j];
        i++; j++;
    }
    a[i] = '\0';
}

void reverse(char *s) {
    int l = length(s);
    for (int i = 0; i < l / 2; i++) {
        char t = s[i];
        s[i] = s[l - i - 1];
        s[l - i - 1] = t;
    }
}

void toUpper(char *s) {
    int i = 0;
    while (s[i] != '\0') {
        if (s[i] >= 'a' && s[i] <= 'z')
            s[i] = s[i] - 32;
        i++;
    }
}

void insert(char *a, char *b, int pos) {
    int la = length(a);
    int lb = length(b);
    for (int i = la; i >= pos; i--)
        a[i + lb] = a[i];
    for (int i = 0; i < lb; i++)
        a[pos + i] = b[i];
}

int main() {
    char str1[200], str2[100];
    int choice, pos;

    do {
        cout << "\n1.Address\n2.Concat\n3.Compare\n4.Length\n5.Upper\n6.Reverse\n7.Insert\n8.Exit\n";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter string: ";
                cin >> str1;
                for (int i = 0; str1[i] != '\0'; i++)
                    cout << str1[i] << " : " << (void*)&str1[i] << endl;
                break;

            case 2:
                cout << "Enter first string: ";
                cin >> str1;
                cout << "Enter second string: ";
                cin >> str2;
                concatenate(str1, str2);
                cout << str1;
                break;

            case 3:
                cout << "Enter first string: ";
                cin >> str1;
                cout << "Enter second string: ";
                cin >> str2;
                if (compare(str1, str2) == 0)
                    cout << "Equal";
                else
                    cout << "Not Equal";
                break;

            case 4:
                cout << "Enter string: ";
                cin >> str1;
                cout << length(str1);
                break;

            case 5:
                cout << "Enter string: ";
                cin >> str1;
                toUpper(str1);
                cout << str1;
                break;

            case 6:
                cout << "Enter string: ";
                cin >> str1;
                reverse(str1);
                cout << str1;
                break;

            case 7:
                cout << "Enter main string: ";
                cin >> str1;
                cout << "Enter string to insert: ";
                cin >> str2;
                cout << "Enter position: ";
                cin >> pos;
                insert(str1, str2, pos);
                cout << str1;
                break;
        }
    } while (choice != 8);

    return 0;
}
```

### 5.  Write a program to merge two ordered arrays to get a single ordered array.



```cpp
#include <iostream>
using namespace std;

int main() {
    int a[100], b[100], c[200];
    int n, m;

    cin >> n;
    for (int i = 0; i < n; i++) cin >> a[i];

    cin >> m;
    for (int i = 0; i < m; i++) cin >> b[i];

    int i = 0, j = 0, k = 0;

    while (i < n && j < m) {
        if (a[i] < b[j])
            c[k++] = a[i++];
        else
            c[k++] = b[j++];
    }

    while (i < n)
        c[k++] = a[i++];

    while (j < m)
        c[k++] = b[j++];

    for (int i = 0; i < k; i++)
        cout << c[i] << " ";

    return 0;
}
```

### 6. Write a program to search a given element in a set of N numbers using Binary search
a. with recursion
b. without recursion.

```cpp
#include <iostream>
using namespace std;

int binarySearchRecursive(int arr[], int left, int right, int key) {
    if (left > right) return -1;
    int mid = (left + right) / 2;
    if (arr[mid] == key) return mid;
    if (key < arr[mid])
        return binarySearchRecursive(arr, left, mid - 1, key);
    else
        return binarySearchRecursive(arr, mid + 1, right, key);
}

int binarySearchIterative(int arr[], int n, int key) {
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = (left + right) / 2;
        if (arr[mid] == key) return mid;
        if (key < arr[mid])
            right = mid - 1;
        else
            left = mid + 1;
    }
    return -1;
}

int main() {
    int n, key, arr[100];

    cin >> n;
    for (int i = 0; i < n; i++) cin >> arr[i];

    cin >> key;

    int r = binarySearchRecursive(arr, 0, n - 1, key);
    int i = binarySearchIterative(arr, n, key);

    if (r != -1)
        cout << "Recursive: Found at index " << r << endl;
    else
        cout << "Recursive: Not found" << endl;

    if (i != -1)
        cout << "Iterative: Found at index " << i << endl;
    else
        cout << "Iterative: Not found" << endl;

    return 0;
}
```

### 7. Write a program to calculate GCD of two numbers
a. with recursion
b. without recursion

```cpp
#include <iostream>
using namespace std;

int gcdRecursive(int a, int b) {
    if (b == 0) return a;
    return gcdRecursive(b, a % b);
}

int gcdIterative(int a, int b) {
    while (b != 0) {
        int t = b;
        b = a % b;
        a = t;
    }
    return a;
}

int main() {
    int a, b;
    cin >> a >> b;

    cout << "Recursive GCD: " << gcdRecursive(a, b) << endl;
    cout << "Iterative GCD: " << gcdIterative(a, b) << endl;

    return 0;
}
```

### 8. Create a Matrix class. Write a menu-driven program to perform following Matrix
operations (exceptions should be thrown by the functions if matrices passed to them are
incompatible and handled by the main() function):
a. Sum
b. Product
c. Transpose

```cpp
#include <iostream>
using namespace std;

class Matrix {
    int r, c;
    int a[10][10];

public:
    void input() {
        cin >> r >> c;
        for (int i = 0; i < r; i++)
            for (int j = 0; j < c; j++)
                cin >> a[i][j];
    }

    void display() {
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++)
                cout << a[i][j] << " ";
            cout << endl;
        }
    }

    Matrix add(Matrix m) {
        if (r != m.r || c != m.c) throw "Addition not possible";
        Matrix res;
        res.r = r;
        res.c = c;
        for (int i = 0; i < r; i++)
            for (int j = 0; j < c; j++)
                res.a[i][j] = a[i][j] + m.a[i][j];
        return res;
    }

    Matrix multiply(Matrix m) {
        if (c != m.r) throw "Multiplication not possible";
        Matrix res;
        res.r = r;
        res.c = m.c;
        for (int i = 0; i < res.r; i++) {
            for (int j = 0; j < res.c; j++) {
                res.a[i][j] = 0;
                for (int k = 0; k < c; k++)
                    res.a[i][j] += a[i][k] * m.a[k][j];
            }
        }
        return res;
    }

    Matrix transpose() {
        Matrix res;
        res.r = c;
        res.c = r;
        for (int i = 0; i < r; i++)
            for (int j = 0; j < c; j++)
                res.a[j][i] = a[i][j];
        return res;
    }
};

int main() {
    Matrix m1, m2, result;
    int choice;

    do {
        cout << "\n1.Sum\n2.Product\n3.Transpose\n4.Exit\n";
        cin >> choice;

        try {
            switch (choice) {
                case 1:
                    m1.input();
                    m2.input();
                    result = m1.add(m2);
                    result.display();
                    break;

                case 2:
                    m1.input();
                    m2.input();
                    result = m1.multiply(m2);
                    result.display();
                    break;

                case 3:
                    m1.input();
                    result = m1.transpose();
                    result.display();
                    break;
            }
        } catch (const char* msg) {
            cout << msg << endl;
        }

    } while (choice != 4);

    return 0;
}
```
#### 9. Define a class Person having name as a data member. Inherit two classes Student and
Employee from Person. Student has additional attributes as course, marks and year and
Employee has department and salary. Write display() method in all the three classes to
display the corresponding attributes. Provide the necessary methods to show runtime
polymorphism

```cpp
