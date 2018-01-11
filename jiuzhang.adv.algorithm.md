## 144. Interleaving Positive and Negative Numbers


## 390. [Find Peak Element II](http://www.lintcode.com/en/problem/find-peak-element-ii/)
[MIT lecture](http://courses.csail.mit.edu/6.006/spring11/lectures/lec02.pdf)
- find the peak value in A[x...][mid] and A[mid][y...]
- search near the peak value

# 7


## 404. [Subarray Sum II](http://www.lintcode.com/en/problem/subarray-sum-ii/)
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
