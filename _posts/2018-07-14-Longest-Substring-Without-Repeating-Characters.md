---
layout : post
title : Longest Substring Without Repeating Characters
category : Algorithms
tags: [Algorithms, Strings]
---

Given a string, find the length of the longest substring without repeating characters.

```markdown
# Example

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", which the length is 1.

Given "pwwkew", the answer is "wke", with the length is 3.
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```



### Solution

<중복된 문자가 없는 가장 긴 부분문자열 길이찾기>

먼저, 키(문자), 값(위치)를 저장할 수 있는 hashmap을 만든다.

그리고 가장 긴 부분문자열을 정의하기 위한 두 포인터를 만든다.

왼쪽포인터는 첫자리에 위치하고, 오른쪽 포인터는 문자를 스캔하면서 hashmap의 값들을 업데이트할 것이다.

왼쪽포인터와 같은 문자가 hashmap에 있다면 왼쪽 포인터는 그 위치를 값으로 업데이트하고



The basic idea is, keep a hashmap which stores the characters in string as keys and their positions as values, and keep two pointers which define the max substring. Move the right pointer to scan through the string, and meanwhile update the hashmap. If the character is already in the hashmap, then move the left pointer to the right of the same character last found. Note that the two pointers can only move forward.

```java
//Java
import java.util.HashMap;


public static int lengthOfLongestSubstring(String s) {
	if(s.length() == 0) {
		return 0;
	}
	HashMap<Character, Integer> map = new HashMap<Character, Integer>();
	int max = 0;
	for(int i=0, j=0;i<s.length();++i) {
		if(map.containsKey(s.charAt(i))) {
			j = Math.max(j, map.get(s.charAt(i))+1);
		}
		map.put(s.charAt(i), i);
		max = Math.max(max, i - j + 1);
	}
	return max;
}

```



Time Complexity : **O(N)**

This solution runs in O(N) time complexity where N is the size of the string.



Space Complexity: **O(N)**

This algorithm uses an extra space of size N.



```markdown
Source by Data Structures & Coding Interview Algorithms, Jaypee
```