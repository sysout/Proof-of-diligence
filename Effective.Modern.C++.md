## Chapter 1
Are you interested in why const member functions should be thread safe
why you should avoid default capture modes in lambda expressions

When an object is initialized with another object of the same type, the new object is said to be a copy of the initializing object, even if the copy was created via the move constructor. Regrettably, there’s no terminology in C++ that distinguishes between an object that’s a copy-constructed copy and one that’s a move-constructed copy:
```cpp
void someFunc(Widget w);
Widget wid;
someFunc(wid); // w is a copy of wid that's created via copy construction
someFunc(std::move(wid)); // w is a copy of wid that's created via move construction
```


When I refer to a function object, I usually mean an object of a type supporting an operator() member function

function objects v.s. callable objects

### item 1 type deduction
Case 1: ParamType is a Reference or Pointer, but not a Universal Reference
1. If expr’s type is a reference, ignore the reference part.
2. Then pattern-match expr’s type against ParamType to determine T.

```cpp
template<typename T>
void f(T& param);
int x = 27;
const int cx = x;
const int& rx = x;
f(x);
f(cx);
f(rx);

template<typename T>
void f(const T& param);
f(x);
f(cx);
f(rx);

template<typename T>
void f(T* param);
int x = 27;
const int *px = &x;
f(&x);
f(px);
```
Case 2: ParamType is a Universal Reference
1. If expr is an lvalue, both T and ParamType are deduced to be lvalue references. First, it’s the only situation in template type deduction where T is deduced to be a reference. Second, although ParamType is declared using the syntax for an rvalue reference, its deduced type is an lvalue reference.
2. If expr is an rvalue, the “normal” (i.e., Case 1) rules apply.

```cpp
template<typename T>
void f(T&& param);
int x = 27;
const int cx = x;
const int& rx = x;
f(x);
f(cx);
f(rx);
f(27);
```
Case 3: ParamType is Neither a Pointer nor a Reference - pass-by-
value

```cpp
template<typename T>
void f(T param);
int x = 27;
const int cx = x;
const int& rx = x;
f(x);
f(cx);
f(rx);
const char* const ptr = "Fun with pointers";
f(ptr);
```

Array Arguments
```cpp
const char name[] = "J. P. Briggs";
const char * ptrToName = name;
template<typename T>
void f(T param);
f(name);

template<typename T>
void f(T& param);
f(name);

template<typename T, std::size_t N>
constexpr std::size_t arraySize(T (&)[N]) noexcept {
  return N;
}
int keyVals[] = { 1, 3, 7, 9, 11, 22, 35 };
int mappedVals[arraySize(keyVals)];
std::array<int, arraySize(keyVals)> mappedVals;
```

Function Arguments
```cpp
void someFunc(int, double);
template<typename T>
void f1(T param);

template<typename T>
void f2(T& param);

f1(someFunc);
f2(someFunc);

```

Things to Remember
- During template type deduction, arguments that are references are treated as non-references, i.e., their reference-ness is ignored.
- When deducing types for universal reference parameters, lvalue arguments get special treatment.
- Whendeducingtypesforby-valueparameters,constand/orvolatileargu‐ ments are treated as non-const and non-volatile.
- During template type deduction, arguments that are array or function names decay to pointers, unless they’re used to initialize references.


### Item 2: Understand auto type deduction.
So the only real difference between auto and template type deduction is that auto assumes that a braced initializer represents a std::initializer_list, but template type deduction doesn’t.

C++14 permits auto to indicate that a function’s return type should be deduced
(see Item 3), and C++14 lambdas may use auto in parameter declarations. However, these uses of auto employ template type deduction, not auto type deduction. So a function with an auto return type that returns a braced initializer won’t compile.
```cpp
auto x = 27;

template<typename T>
void func_for_x(T param);
func_for_x(27);

const auto cx = x;
template<typename T>
void func_for_cx(const T param);
func_for_cx(x);

const auto& rx = x;
template<typename T>
void func_for_rx(const T& param);
func_for_rx(x);

auto&& uref1 = x;
auto&& uref2 = cx;
auto&& uref3 = 27;

const char name[] = "R. N. Briggs";
auto arr1 = name;
auto& arr2 = name;
void someFunc(int, double);
auto func1 = someFunc;
auto& func2 = someFunc;

// type is int, value is 27
auto x1 = 27;
auto x2(27);
// type is std::initializer_list<int>, value is { 27 }
auto x3 = { 27 };
auto x4{ 27 };

auto createInitList() {
  return { 1, 2, 3 }; // error: can't deduce type
}
```
Things to Remember
- auto type deduction is usually the same as template type deduction, but auto type deduction assumes that a braced initializer represents a std::initial izer_list, and template type deduction doesn’t.
- auto in a function return type or a lambda parameter implies template type deduction, not auto type deduction.

### Item 3: Understand decltype
```cpp
// C++11
template<typename Container, typename Index>
auto authAndAccess(Container& c, Index i) -> decltype(c[i])
{
  authenticateUser();
  return c[i];
}

// C++14 not quite correct
template<typename Container, typename Index>
auto authAndAccess(Container& c, Index i)
{
  authenticateUser();
  return c[i];
}

// C++14; works, but still requires refinement
template<typename Container, typename Index>
decltype(auto)
authAndAccess(Container& c, Index i)
{
  authenticateUser();
  return c[i];
}

// final C++14 version
template<typename Container, typename Index>
decltype(auto)
authAndAccess(Container&& c, Index i)
{
  authenticateUser();
  return std::forward<Container>(c)[i];
}

// final C++11 version
template<typename Container, typename Index>
auto
authAndAccess(Container&& c, Index i)
-> decltype(std::forward<Container>(c)[i])
{
  authenticateUser();
  return std::forward<Container>(c)[i];
}

Widget w;
const Widget& cw = w;
auto myWidget1 = cw;  // myWidget1's type is Widget
decltype(auto) myWidget2 = cw; // myWidget1's type is const Widget&

```
That is, if an lvalue expression other than a name has type T, decltype reports that type as T&.
```cpp
decltype(auto) f1() {
  int x = 0;
  return x;
}
decltype(auto) f2() {
  int x = 0;
  return (x);
}
```
Things to Remember
- decltype almost always yields the type of a variable or expression without any modifications.
- For lvalue expressions of type T other than names, decltype always reports a type of T&.
- C++14 supports decltype(auto), which, like auto, deduces a type from its initializer, but it performs the type deduction using the decltype rules.

### Item 4: Know how to view deduced types.
```cpp
const int theAnswer = 42;
auto x = theAnswer;
auto y = &theAnswer;


template<typename T>
class TD;
TD<decltype(x)> xType;


std::vector<Widget> createVec();
const auto vw = createVec();
if (!vw.empty()) {
  f(&vw[0]){
    ...
  };
}

#include <boost/type_index.hpp>
template<typename T>
void f(const T& param)
{
  using std::cout;
  using boost::typeindex::type_id_with_cvr;
  // show T
  cout << "T = "
      << type_id_with_cvr<T>().pretty_name()
      << '\n';

  // show param's type
  cout << "param = "
      << type_id_with_cvr<decltype(param)>().pretty_name()
      << '\n';
}
```
Things to Remember
- Deduced types can often be seen using IDE editors, compiler error messages, and the Boost TypeIndex library.
- The results of some tools may be neither helpful nor accurate, so an understanding of C++’s type deduction rules remains essential.

### Item 5: Prefer auto to explicit type declarations
Things to Remember
- auto variables must be initialized, are generally immune to type mismatches that can lead to portability or efficiency problems, can ease the process of refactoring, and typically require less typing than variables with explicitly specified types.
- auto-typed variables are subject to the pitfalls described in Items 2 and 6.

### Item 6: Use the explicitly typed initializer idiom when auto deduces undesired types
