## Online compiler
- https://wandbox.org/

## [Functional Programming using C++](https://www.udemy.com/functional-programming-using-cpp/)

## [Mastering C++ Standard Library Features](https://www.udemy.com/mastering-c-standard-library-features/)

## [Data Structures and Algorithms in C++ For Coding Interview!](https://www.udemy.com/data-structures-and-algorithms-cplusplus-for-interviews/learn/v4/overview)
- [Two Sum](https://leetcode.com/problems/two-sum/description/)
  * `vector<pair<int, int>> vec;`
  * `sort(vec.begin(), vec.end());`
  * `return vector<int>{vec[i].second, vec[j].second};`
- [Valid Parentheses](https://leetcode.com/submissions/detail/156341620/)
  * `s.find("()") != string::npos`
  * `s.replace(s.find("()"), 2, "")`
- [682. Baseball Game](https://leetcode.com/problems/baseball-game/description/)
  * `stack<int> st;`
  * `st.pop();`
  * `st.top()`
  * `st.push(top);`
- [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/description/)
  * `map.find(nums[i]) != map.end()`
- [373. Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/description/)
  * `priority_queue<pair<int, int>, vector<pair<int, int>>, mycompare> pq;`

## coding tips
- [brace initialization](https://stackoverflow.com/questions/18222926/why-is-list-initialization-using-curly-braces-better-than-the-alternatives)
- [C++ Braced Initialization](http://blog.quasardb.net/cpp-braced-initialization/)
- [why does std::stack::pop() returns void?](http://cpptruths.blogspot.com/2005/10/why-does-stdstackpop-returns-void.html)
- [array initialization](https://stackoverflow.com/questions/201101/how-to-initialize-all-members-of-an-array-to-the-same-value)
  * `int arr[100] = {}`
  * `vector<int> vec(100, 0)`
- [operator[] will insert an entry for you with a default-constructed value, if one isn't already there](https://stackoverflow.com/questions/6897737/using-the-operator-efficiently-with-c-unordered-map)
- [priority_queue](https://en.cppreference.com/w/cpp/container/priority_queue)
  * min pq: `priority_queue<int, vector<int>, greater<int>> pq;`
  * std::less
  * std::greater
  * std::less_equal
  * std::greater_equal
- static_cast<int>(data)

  ```cpp
  char c = 10;
  int *q = static_cast<int*>(&c); // compile-time error
  ```

## Overload Resolution
Ansel Sermersheim & Barbara Geller
ACCU / C++
June 2018
- introduction
  * Function overloading
  * free functions, constructors, and methods
  * disregard the return type

## Exception
- setjump/longjump EH
- Table Based EH - (gcc style)
  * stop tracking state in the happy path
  * gcc_except_table
    + describe what to do while walking in the stack

### [Modern C++](https://www.youtube.com/watch?v=1QT9HnCkz4I&list=PL9GxRn_rQx8Pwe4bMecruWbIEICAsZtgT)

### [data types](https://www.youtube.com/watch?v=1QT9HnCkz4I&index=1&list=PL9GxRn_rQx8Pwe4bMecruWbIEICAsZtgT)
- [Method pointer data type](https://youtu.be/1QT9HnCkz4I?list=PL9GxRn_rQx8Pwe4bMecruWbIEICAsZtgT&t=733)

  ```cpp
  bool (Widget::* myMethod) (int, int);
  Widget foo;
  bool data = (foo->*myMethod)(row, col);
  // declaration and initialization
  int (MyClass::*ptr)(double) = &MyClass::myMethod;
  ```

- Lambda data type : [capture list] (parameter list) -> returnType {body};
  * capture list
    + C++11 has capture by value or reference
    + C++14 added capture by move
    + C++17 adds the ability to capture \*this by value

    ```cpp
    int main()
    {
        int var{47};
        auto lamb = [var](){
            std::cout << "Hello " << var << std::endl;
        };
        var = 7;
        lamb();
    }
    ```

### [https://www.youtube.com/watch?v=j9arNRRoPe8](https://youtu.be/j9arNRRoPe8?t=2822)

```cpp
//
// Created by Xiong Xiong on 7/4/18.
//

#include <iostream>
#include <memory>
#include <string>
#include <stdio.h>
#include <functional>

using namespace std;

struct Address {
    string *house_name = nullptr;
};

struct Person {
    Address *address = nullptr;
};

template<typename T>
struct Maybe;

template<typename T>
Maybe<T> maybe(T *context) {
    return Maybe<T>(context);
};

template<typename T>
struct Maybe {
    T *context;

    Maybe(T *context) : context{context} {};

    template<typename Func>
    auto with(Func exe) {
        return context != nullptr ? maybe(exe(context)) : nullptr;
    }

    template<typename Func>
    auto doit(Func exe) {
        if (context != nullptr) {
            exe(context);
        }
        return *this;
    }
};

void print_house_name(Person *p) {
    maybe(p)
            .with([](auto v) { return v->address; })
            .with([](auto v) { return v->house_name; })
            .doit([](auto v) { cout << *v << endl; });
}

int main() {
    Person *p = new Person{};
    p->address = new Address{};
    p->address->house_name = new string{"Hello"};
    print_house_name(p);
    delete p->address->house_name;
    delete p->address;
    delete p;
}
```

## What does this mean?
- http://www.cplusplus.com/reference/utility/make_pair/
  - Data races: If either (or both) T1 or T2 is an rvalue reference type of a type supporting move semantics, its corresponding argument is modified.


## Mastering the C++17 STL
### Chapter 3 The Iterator-Pair Algorithms
#### Shunting data with std::copy
```cpp
#include <boost/iterator/iterator_facade.hpp>

class putc_iterator : public boost::iterator_facade<
    putc_iterator,
    const putc_iterator,
    std::output_iterator_tag>{
        friend class boost::iterator_core_access;
        auto& dereference() const {return * this;}
        void increment(){}
        bool equal(const putc_iterator&) const {return false;}
        public:
        void operator=(char ch) const {putc(ch, stdout);}
    };
int main()
{   
    std::string s{"hello"};
    std::copy(s.begin(), s.end(), putc_iterator{});
}
```

```cpp
#include <iostream>
#include <vector>
#include <cassert>

namespace std{
    template <class Container>
    class back_insert_iterator2{
    using CtrValueType = typename Container::value_type;
    Container *c;
    public:
    using iterator_category = output_iterator_tag;
    using difference_type = void;
    using value_type = void;
    using pointer = void;
    using reference = void;
    explicit back_insert_iterator2(Container& ctr): c(&ctr){}
    auto& operator*() {return *this;}
    auto& operator++() {return *this;}
    auto& operator++(int) {return *this;}
    auto& operator=(const CtrValueType& v) {
        c->push_back(v);
        cout<<c->size()<<'\n';
        return *this;
    }
    auto& operator=(CtrValueType&& v){
        c->push_back(move(v));
        return *this;
    }
    };

    template<class Container>
    auto back_inserter2(Container& c){
        // works for C+17: Template argument deduction for class templates
        // return back_insert_iterator2(c);
        return back_insert_iterator2<Container>(c); // works for C+14
    }
}

int main(){
    std::string s{"hello"};
    std::vector<char> dest;
    std::copy(s.begin(), s.end(), std::back_inserter2(dest));
    assert(dest.size() == 5);
}
```

- [Perfect Forwarding: The Solution](http://thbecker.net/articles/rvalue_references/section_08.html)

```cpp
#include <iostream>
using namespace std;

template<class T1, class T2>
void print_is_same() {
  std::cout << std::is_same<T1, T2>() << '\n';
}

template<typename Arg>
void foo(Arg&& v){
    print_is_same<int, Arg>();
    print_is_same<int&, Arg>();
    print_is_same<int&&, Arg>();
    cout << v << endl;
};

int main(){
    std::cout << std::boolalpha;
    int x = 1;
    foo(x);
    foo(1);
}
```

- [copy elision and return value optimization?](https://stackoverflow.com/questions/12953127/what-are-copy-elision-and-return-value-optimization)


## Named Arguments from Scratch
Boost Hana
-std=c++17 -O3
```cpp
#include <string>
#include <boost/hana.hpp>
namespace hana = boost::hana;
using namespace hana::literals;

static int foo(int a, float b, std::string const& c){
  return (c.size() + a) / b;
}

constexpr auto extract = [](auto args){
  return hana::make_tuple(
    args[2_c],
    args[1_c],
    args[0_c]
  );
}

int main(){
  auto args = hana::make_tuple(
    "hello world",
    0.5,
    10
  );
  auto arg_pack = extract(args);
  return hana::unpack(args, foo);
}
```


```cpp
#include <string>
#include <boost/hana.hpp>
namespace hana = boost::hana;
using namespace hana::literals;

static int foo(int a, float b, std::string const& c){
  return (c.size() + a) / b;
}

constexpr auto extract = [](auto arg_spec, auto args){
  return hana::transform(arg_spec, [args](auto key) {
    return args[key]
  };
};

int main(){
  auto arg_spec = hana::make_tuple(
    0_c,
    1_c,
    2_c
  );
  auto args = hana::make_map(
    hana::make_pair(2_c, "hello world"),
    hana::make_pair(1_c, 0.5),
    hana::make_pair(0_c, 10)
  );
  auto arg_pack = extract(arg_spec, args);
  return hana::unpack(arg_pack, foo);
}
```


```cpp
#include <string>
#include <boost/hana.hpp>
namespace hana = boost::hana;
using namespace hana::literals;

static int foo(int a, float b, std::string const& c){
  return (c.size() + a) / b;
}

constexpr auto extract = [](auto arg_spec, auto args){
  return hana::transform(arg_spec, [args](auto key) {
    return args[key]
  };
};

template<typename CharT, CharT... Chars>
constexpr auto operator"" _arg() -> hana::string<Chars...>{
  return {};
}

constexpr auto compose = [](auto&& f, auto arg_spec, auto... input_args){
  auto args = hana::make_map(input_args...);
  auto arg_pack = extract(arg_spec, args);
  return haha::unpack(arg_pack, f);
}

int main(){
  auto arg_spec = hana::make_tuple(
    "a"_arg,
    "b"_arg,
    "c"_arg
  );
  return compose(foo, arg_spec,
    hana::make_pair("c"_arg, "hello world"),
    hana::make_pair("b"_arg, 0.5),
    hana::make_pair("a"_arg, 1),
}
```



```cpp
#include <string>
#include <boost/hana.hpp>
namespace hana = boost::hana;
using namespace hana::literals;

static int foo(int a, float b, std::string const& c){
  return (c.size() + a) / b;
}

constexpr auto extract = [](auto arg_spec, auto args){
  return hana::transform(arg_spec, [args](auto key) {
    return args[key]
  };
};

template<typename CharT, CharT... Chars>
constexpr auto operator"" _arg() -> hana::string<Chars...>{
  return {};
}

constexpr auto adapt = [](auto const& f, auto... args_for_spec){
  auto arg_spec = hana::make_tuple(args_for_spec...);
  return [&f, arg_spec](auto... input_args){
    auto args
  }
}

constexpr auto compose = [](auto&& f, auto arg_spec, auto... input_args){
  auto args = hana::make_map(input_args...);
  auto arg_pack = extract(arg_spec, args);
  return haha::unpack(arg_pack, f);
}


int main(){
  auto my_foo = adapt(foo,
    "a"_arg,
    "b"_arg,
    "c"_arg
  );
  return compose(foo, arg_spec,
    hana::make_pair("c"_arg, "hello world"),
    hana::make_pair("b"_arg, 0.5),
    hana::make_pair("a"_arg, 1),
}
```
