SOLID:
- Single responsibility principle
- Open close principle: open to extension, close to modification
- Liskov substitution principle: subclass can replace parent class
- Interface segregation principle
- Dependency inversion principle

5C template
- Clarify
  * what: use keywords to ask questions
  * how
  * who
- Core object
- Cases
- Classes
- Correctness

[OOD UML access modifier](http://javajee.com/important-uml-diagrams-required-to-work-with-design-patterns)
- \~ default
- \+ public
- \- private
- \# protected

## jiuzhang advanced algorithm
### Chapter 1
- moving window with two pointer
  * The core of these questions are
    + `how to check the valid state efficiently`
    + maintain a consistent state
      - if the state is not valid at the beginning `find a valid state in while loop`
      - if the state is valid at the beginning `keep a valid state through out the for & while loop`
  ```java
  int ans = Integer.MAX_VALUE;
  for (int lo = 0, hi = 0, sum = 0; lo < nums.length; lo++){
      while (sum < s && hi < nums.length){
          sum += nums[hi++];
      }
      if (sum >= s){
          ans = Math.min(ans, hi - lo);
      }
      sum -= nums[lo];
  }
  return ans == Integer.MAX_VALUE ? -1 : ans;
  ```
  * [406. Minimum Size Subarray Sum](http://www.lintcode.com/en/problem/minimum-size-subarray-sum/)
    + valid condition: `sum >= s`
  * [32. Minimum Window Substring](http://www.lintcode.com/en/problem/minimum-window-substring/)
    + valid condition `validLen >= target.length()`
  * [384. Longest Substring Without Repeating Characters](http://www.lintcode.com/en/problem/longest-substring-without-repeating-characters/)
    + valid condition `map[cur] == false`
  * [386. Longest Substring with At Most K Distinct Characters](http://www.lintcode.com/en/problem/longest-substring-with-at-most-k-distinct-characters/)
    + `always keep hi pointing to a valid state in the while loop`
- Kth Smallest Number in Arrays / Matrix
  * `***`[401. Kth Smallest Number in Sorted Matrix](http://www.lintcode.com/en/problem/kth-smallest-number-in-sorted-matrix/)
    + hard: `divide & conquer`
    + tricky part: `return left;`
  * [543. Kth Largest in N Arrays](http://www.lintcode.com/en/problem/kth-largest-in-n-arrays/)
    + think about when k > average array length
    + naive pq method: `n * m * log(k)`
    + improve method: `n * m * log(m) + k * log(k)`
  * `***`[465. Kth Smallest Sum In Two Sorted Arrays](http://www.lintcode.com/en/problem/kth-smallest-sum-in-two-sorted-arrays/)
    + `visualize two arrays as a sorted matrix`


### Chapter 2 data structure
- Union Find
  * [589. Connecting Graph](http://www.lintcode.com/en/problem/connecting-graph/)
  * `*`[590. Connecting Graph II](http://www.lintcode.com/en/problem/connecting-graph-ii/)
  * [591. Connecting Graph III](http://www.lintcode.com/en/problem/connecting-graph-iii/)
  * `**`[433. Number of Islands](http://www.lintcode.com/en/problem/number-of-islands/)
    + only have to look up the left and up
  * `***`[434. Number of Islands II](http://www.lintcode.com/en/problem/number-of-islands-ii/)
    + always remember `i * m + j`
    + how to handle sparse matrix when both n and m are extremely large: use hashmap instead of int array
  * [178. Graph Valid Tree](http://www.lintcode.com/en/problem/graph-valid-tree/)
  * `**`[477. Surrounded Regions](http://www.lintcode.com/en/problem/surrounded-regions/)
- Trie
  * [442. Implement Trie](http://www.lintcode.com/en/problem/implement-trie/)
  * `*`[473. Add and Search Word](http://www.lintcode.com/en/problem/add-and-search-word/)
  * `**`[132. Word Search II](http://www.lintcode.com/en/problem/word-search-ii/)
  * `***`[634. Word Squares](http://www.lintcode.com/en/problem/word-squares/)
    ```java
    class TrieNode{
        List<String> startWith;
        boolean hasWord;
    }
    ```

#### 144. Interleaving Positive and Negative Numbers


#### 390. [Find Peak Element II](http://www.lintcode.com/en/problem/find-peak-element-ii/)
[MIT lecture](http://courses.csail.mit.edu/6.006/spring11/lectures/lec02.pdf)
- find the peak value in A[x...][mid] and A[mid][y...]
- search near the peak value

#### 404. [Subarray Sum II](http://www.lintcode.com/en/problem/subarray-sum-ii/)
- **九章的答案松松垮垮，下标满天飞，感觉有错，而且也完全记不住**
- binary search
```java
int find(int[] A, int len, int value) {
    if (A[len-1] < value )
        return len;

    int l = 0, r = len-1, ans = 0;
    while (l <= r) {
        int mid = (l + r) / 2;
        if (value <= A[mid]) {
            ans = mid;
            r = mid - 1;
        }  else
            l = mid + 1;
    }
    return ans;
}
```

## Extra
- [Segment Tree](http://www.lintcode.com/en/tag/segment-tree/)
  * [439. Segment Tree Build II](http://lintcode.com/en/problem/segment-tree-build-ii/)
  * [247. Segment Tree Query II](http://lintcode.com/en/problem/segment-tree-query-ii/)
  * [203. Segment Tree Modify](http://www.lintcode.com/en/problem/segment-tree-modify/)
  * `**` [207. Interval Sum II](http://www.lintcode.com/en/problem/interval-sum-ii/)
  * `***`[249. Count of Smaller Number before itself](http://www.lintcode.com/en/problem/count-of-smaller-number-before-itself/)

## leetcode contest
- [Weekly Contest 68](https://leetcode.com/contest/weekly-contest-68/)
  * [766. Toeplitz Matrix](https://leetcode.com/contest/weekly-contest-68/problems/toeplitz-matrix/)
  ```java
  public boolean isToeplitzMatrix(int[][] matrix) {
      for (int i = 0; i < matrix.length - 1; i++) {
          for (int j = 0; j < matrix[i].length - 1; j++) {
              if (matrix[i][j] != matrix[i + 1][j + 1]) return false;
          }
      }
      return true;
  }
  ```
  * [767. Reorganize String](https://leetcode.com/contest/weekly-contest-68/problems/reorganize-string/)
  * [769. Max Chunks To Make Sorted (ver. 1)](https://leetcode.com/contest/weekly-contest-68/problems/max-chunks-to-make-sorted-ver-1/)
  * [768. Max Chunks to Make Sorted (ver. 2)](https://leetcode.com/contest/weekly-contest-68/problems/max-chunks-to-make-sorted-ver-2/)
    + Same solution for two problem: [Java solution, left max and right min.](https://discuss.leetcode.com/topic/117872/java-solution-left-max-and-right-min)
  * [770. Basic Calculator IV](https://leetcode.com/contest/weekly-contest-68/problems/basic-calculator-iv/)

- [Weekly Contest 69](https://leetcode.com/contest/weekly-contest-69)
  * `***`[773. Sliding Puzzle](https://leetcode.com/contest/weekly-contest-69/problems/sliding-puzzle/)
    + [construct the next permutation in lexicographic order](https://www.quora.com/How-would-you-explain-an-algorithm-that-generates-permutations-using-lexicographic-ordering)
      - Find the largest x such that P[x]<P[x+1].
        * (If there is no such x, P is the last permutation.)
      - Find the largest y such that P[x]<P[y].
      - Swap P[x] and P[y].
      - Reverse P[x+1 .. n].
      - [video demo](https://www.youtube.com/watch?v=goUlyp4rwiU)
    + `Permutation Encoding` copied from uwi
    ```java
     public int encPerm(int[] a)
     {
       int n = a.length;
       int used = 0;
       int ret = 0;
       for(int i = 0;i < n;i++){
         ret = ret * (n - i) + a[i] - Integer.bitCount(used & ((1<<a[i]) - 1));
         used |= 1<<a[i];
       }
       return ret;
     }
    ```
    + `***`[My submission](https://leetcode.com/submissions/detail/138297283/): Runtime: 10 ms
    + [simple BFS implementation](https://discuss.leetcode.com/topic/118770/java-19ms-28-clean-lines-bfs-with-comment)
      ```java
      for (int sz = q.size(); sz > 0; --sz) {
      }
      ```
  * `**`[774. Minimize Max Distance to Gas Station](https://leetcode.com/contest/weekly-contest-69/problems/minimize-max-distance-to-gas-station/)
    + When you see the question accept an approximate result as the answer, you know it's `divide and conquer`
    ```java
    while (lo + 1e-6 < hi){}
    ```

## lintcode contest
- [Weekly Contest 1]
- [Weekly Contest 2]
  * [782. AND and OR](http://lintcode.com/en/problem/and-and-or/)
  * `***` [783. Minimum Risk Path](http://lintcode.com/en/problem/minimum-risk-path/)
    + 通过 Kruskal 算法，将含有位置 0 结点的子树和含有位置 n 结点的子树合并时的那条边的权值为答案。
    + UnionFind实际应用
