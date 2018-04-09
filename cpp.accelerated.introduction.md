## [Accelerated Introduction to C++](https://app.pluralsight.com/library/courses/accelerated-introduction-cpp/table-of-contents)
by Dmitri Nesteruk

## [Installing G++ on a Mac](http://www-scf.usc.edu/~csci104/20142/installation/gccmac.html)

```bash
clang++ -std=c++11 -stdlib=libc++ -Weverything main.cpp
# or simply
g++-7 main.cpp
```

### Basics
- Numeric types get auto-converted (0 = false, none-0 = true)

### Pointers

```cpp
float *n; // no default value, n is not null, it has a random value
float *n = &u;
float *n = nullptr; // no default value
float f = *n; // dereference
int* x, y; // declare a pointer and a int
```
### reference
- No concept of a 'null' reference
- Pointer to reference is illegal
  * reference can't stored in containers
  * std::reference_wrapper

```cpp
int &x = y; // x is a reference to y
int *n;
int &m = *n; // reference to pointer
```

### Arrays
- when passing a c style array, array length has to be passed separately.
- std::array
- std::vector
- [Array initialization](http://en.cppreference.com/w/c/language/array_initialization)

```cpp
int numbers[]{1,2,3}; // c style array, can't tell the length of the array
int zeros[10]{0}; // length is 10, first element is 0
array<int, 3> values{1,2,3};
values.size();

// Array initialization
int x[] = {1,2,3}; // x has type int[3] and holds 1,2,3
int y[5] = {1,2,3}; // y has type int[5] and holds 1,2,3,0,0
int z[3] = {0}; // z has type int[3] and holds all zeroes

// designator (since C99), [4]= is the designator
int n[5] = {[4]=5,[0]=1,2,3,4} // holds 1,2,3,4,5

int a[MAX] = { // starts initializing a[0] = 1, a[1] = 3, ...
    1, 3, 5, 7, 9, [MAX-5] = 8, 6, 4, 2, 0
}
// for MAX=6,  array holds 1,8,6,4,2,0
// for MAX=13, array holds 1,3,5,7,9,0,0,0,8,6,4,2,0 ("sparse array")
```

### Character Types
- char
  * `char c = 'z';`
  * 1 byte
- wchar_t
  * the width of wchar_t is compiler specific
  * it's not recommend to use
- char16_t, char32_t
- the char/wchar duality propagates everywhere
  * string/wstring
  * main/wmain
  * cout/wcout

### string
- c style string
  * `char *text = "hello";`
  * zero terminated
- wide characters
  * `wchar_t * text = L"hello";`
- std::string, std::wstring
  * `string s{"hello"};`
  * `int n = s.length();`
  * `string part = s.substr(0, 4);`
  * `s += "world";`
  * `s[0] = 'H';`

### [namespace](https://app.pluralsight.com/player?course=accelerated-introduction-cpp&author=dmitri-nesteruk&name=aicpp-m04&clip=1&mode=live)

```cpp
namespace life{
  auto meaning = 42;
  auto *pr = &meaning;
  auto &rf = meaning
}
using namespace life;
using life::meaning;
```

### [Function](https://app.pluralsight.com/player?course=accelerated-introduction-cpp&author=dmitri-nesteruk&name=aicpp-m04&clip=2&mode=live)

```cpp
inline int add(int a, int b) { return a + b;}
inline auto add2(int a, int b) -> int { return a + b;}
```

### [Lambda Function](https://app.pluralsight.com/player?course=accelerated-introduction-cpp&author=dmitri-nesteruk&name=aicpp-m04&clip=4&mode=live)
- [] lambda does not access enclosing scope
- [=] capture everything by value
- [&] capture everything by reference
- [x, &y] capture x by value, and y by reference
- [&, z] capture everything by reference, but z by value

```
auto doubleV = [](int z) {return z * 2;};
```

### [Iteration](https://app.pluralsight.com/player?course=accelerated-introduction-cpp&author=dmitri-nesteruk&name=aicpp-m05&clip=1&mode=live)

```cpp
int main(int argc, char* argv[]){
  using namespace std;
  int a[]={1,2,3,4};
  for (int *p = a, *e = a + 4; p != e; p++){
    cout << *p << endl;
  }
  auto ba = begin(a);
  auto ea = end(a);
  for (; ba != ea; ba++){
    cout << *ba << endl;
  }
  for (auto val : a){
    cout << val << endl;
  }
  std::vector<int> v{1,2,3,4,5};
  auto bv = v.begin(); // begin(v);
  auto cbv = v.cbegin();
  *cbv = 3; // error

  for (auto i = v.rbegin(); i != v.rend(); ++i){
    cout << *i << endl;
  }

  return 0;
}
```

- [Value categories](http://en.cppreference.com/w/cpp/language/value_category)

- [cpp online challenges](https://www.hackerrank.com/domains/cpp/cpp-introduction)
