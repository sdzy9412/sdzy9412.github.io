---
layout: post
title: LeetCode - Two Pointers 
categories: LeetCode
description: Here is description.
keywords: LeetCode, Two Pointers

---



167\. [Two Sum II - Input array is sorted (Easy)](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

Given an array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific `target` number.

Return the indices of the two numbers (1-indexed) as an integer array `answer` of size `2`, where `1 <= answer[0] < answer[1] <= numbers.length`.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

```java
 public int[] twoSum(int[] numbers, int target) {
    int[] result = new int[2];
    int i = 0;
    int end = numbers.length-1;
     for(int j=end;j>i;j--){
         if(numbers[j]+numbers[i]==target) {
             result[0] = i+1;
             result[1] = j+1;
             break;
         }else if(numbers[j]+numbers[i]>target)
             continue;
         else if(numbers[j]+numbers[i]<target) {
             i++;
             j++;
         }
     }
   return result;
}
```

633\. [Sum of Square Numbers (Easy)](https://leetcode.com/problems/sum-of-square-numbers/description/)

Given a non-negative integer `c`, decide whether there're two integers `a` and `b` such that `a2 + b2 = c`.

```java
public boolean judgeSquareSum(int c) {
    int j=(int) Math.sqrt(c);
    int i=0;
    while (i<=j){
        if(i*i+j*j == c){
            return true;
        }else if (i*i+j*j > c){
            j--;
        }else {
            i++;
        }
    }
    return false;
}
```


345\. [Reverse Vowels of a String (Easy)](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)

Given a string `s`, reverse only all the vowels in the string and return it.

The vowels are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`, and they can appear in both cases.

```java
static public String reverseVowels(String s) {
    char[] ch = s.toCharArray();
    int i=0,j=ch.length-1;
    String vowels = "aAeEiIoOuU";
    char temp;
    while(i<j){
        while(i<j&&vowels.indexOf(ch[i])==-1){
            i++;
        }
        while(i<j&&vowels.indexOf(ch[j])==-1){
           j--;
        }
   		     if(i<j&&vowels.indexOf(ch[j])!=-1&&i<j&&vowels.indexOf(ch[i])!=-1) {
            temp = ch[i];
            ch[i] = ch[j];
            ch[j] = temp;
            i++;
            j--;
        }
    }
    String result = String.valueOf(ch);
    return result;
}
```



680\. [Valid Palindrome II (Easy)](https://leetcode.com/problems/valid-palindrome-ii/description/)

Given a string `s`, return `true` *if the* `s` *can be palindrome after deleting **at most one** character from it*.

```java
static public boolean validPalindrome(String s) {
    int i=0,j=s.length()-1;
    int flag =0;
    while(i<j){
        if(s.charAt(i) == s.charAt(j)){
            i++;
            j--;
        }else return (isPalindrome(s,i,j-1) || isPalindrome(s,i+1,j));
    }


    return true;
}

static public boolean isPalindrome(String s,int i, int j) {
    while (i<j){
        if(s.charAt(i++) == s.charAt(j--)) return false;
    }
    return true;
}
```



88\. [Merge Sorted Array (Easy)](https://leetcode.com/problems/merge-sorted-array/description/)

You are given two integer arrays `nums1` and `nums2`, sorted in **non-decreasing order**, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

**Merge** `nums1` and `nums2` into a single array sorted in **non-decreasing order**.

The final sorted array should not be returned by the function, but instead be *stored inside the array* `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.

```java
static public void merge(int[] nums1, int m, int[] nums2, int n) {
    int allLen = nums1.length-1;
    m--;
    n--;
    while(n>=0){
        if(m<0){ //nums1检查完, 放剩下的nums2
            nums1[allLen--] = nums2[n--];
        }else if(n<0){//nums2检查完， 放剩下的nums1
            nums1[allLen--] = nums1[m--];
        }else if(nums1[m]>=nums2[n]){ //nums1 更大
            nums1[allLen--] = nums1[m--];
        }else if(nums1[m]<nums2[n]){ //nums2 更大
            nums1[allLen--] = nums2[n--];
        }
    }
}
```

141\. [Linked List Cycle (Easy)](https://leetcode.com/problems/linked-list-cycle/description/)

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.

Return `true` *if there is a cycle in the linked list*. Otherwise, return `false`.

**Example:**

![image-20210604194958082](C:\Users\sdzy9\AppData\Roaming\Typora\typora-user-images\image-20210604194958082.png)

result: true

```java
static public boolean hasCycle(ListNode head) {
         /* arraylist - 550ms, hashset - 5ms
//        ArrayList arr = new ArrayList();
        HashSet<ListNode> arr = new HashSet<ListNode> ();
        if(head==null || head.next==null) return false;
        while(head.next != null){
            if (arr.contains(head)){
                return true;
            }else {
                arr.add(head);
                head = head.next;
            }
        }
//        System.out.println(arr.toString());
        return false;*/

        //two pointer - 1ms
        if (head==null || head.next == null) {
            return false;
        }
        ListNode l1 = head, l2 = head.next;
        while (l1 != null && l2 != null && l2.next != null) {
            if (l1 == l2) {
                return true;
            }
            l1 = l1.next;
            l2 = l2.next.next;
        }
        return false;
    }
```

524\. [Longest Word in Dictionary through Deleting (Medium)](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/)

Given a string `s` and a string array `dictionary`, return *the longest string in the dictionary that can be formed by deleting some of the given string characters*. If there is more than one possible result, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

```java
static public String findLongestWord(String s, List<String> dictionary) {
    String result = "";
    for(String dic:dictionary){
        if (result.length()>dic.length() || ((result.length()==dic.length())&&(result.compareTo(dic))<0)){
            continue; //跳过 不是需要对比的
        }
        if (isSub(s,dic)){
            result = dic;
        }
    }
    return result;
}
static public boolean isSub(String s, String result){
    int i=0,j=0;
    while (i<s.length() && j<result.length()){
        if(s.charAt(i) == result.charAt(j)){
            j++;
        }
        i++;
    }
    return j==result.length();
}
```

Thanks to [cyc2018.xyz](http://www.cyc2018.xyz/)!

