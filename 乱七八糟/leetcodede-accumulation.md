---
title: leetcodede_accumulation
date: 2020-02-19 17:07:57
tags: leetcode
---

两个有序数组归并为一个有序数组。

```java
class Solution {
    public int[] merge(int[] nums1, int[] nums2) {
        int nums[] = new int[nums1.length + nums2.length];
        int i = nums1.length - 1, j = nums2.length - 1, k = nums1.length + nums2.length - 1;
        while (i >= 0 || j >= 0) {
            nums[k--] = i < 0 ? nums2[j--] : (j < 0 ? nums1[i--] :
                                              (nums1[i] > nums2[j] ? nums1[i--] : nums2[j--]));
        }
        return nums;
    }
}//时间复杂度 m+n；
```

