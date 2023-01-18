# Sort methods：

### Merge Sort (归并排序)
merge sort 的基本思想是把一个数组 ***分为两个子数组***，通过递归的方式重复切分子数组，直到只剩下一个元素。然后俩俩元素比较大小后合并起来，通过不停的合并子数组，最后得到排好序的数组。是 divide and conquer 算法的一种应用。如下图[1]：
![DFS template](../img/Merge_Sort.png)
merge sort 的时间复杂度为 O(nlogN), 空间复杂度为 O(N)。

该排序方法的难点之一在于需要实现一个 merge 方法。
首先我们通过一个 leetcode 题目来熟悉 merge 方法：
* [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)
```Java
public void merge(int[] nums1, int m, int[] nums2, int n) {
  int[] sorted = new int[m + n];
  int p1 = 0, p2 = 0, i = 0;
  while(p1 < m || p2 < n){
      if(p1 == m){
          sorted[i] = nums2[p2];
          p2++;
      } else if(p2 == n){
          sorted[i] = nums1[p1];
          p1++;
      }else if(nums1[p1] < nums2[p2]){
          sorted[i] = nums1[p1];
          p1++;
      } else {
          sorted[i] = nums2[p2];
          p2++;
      }
      i++;
  }
  for(int j = 0; j < m+n; j++){
      nums1[j] = sorted[j];
  }
  }
```
通过双指针实现合并，这里需要使用一个额外的数组来储存，所以空间复杂度为O(n)。


### References
1. 图灵星球TuringPlanet： https://turingplanet.org/2020/02/11/排序算法【数据结构和算法3】/#gui_bing_pai_xu_MergeSort