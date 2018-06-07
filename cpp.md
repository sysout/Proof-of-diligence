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
