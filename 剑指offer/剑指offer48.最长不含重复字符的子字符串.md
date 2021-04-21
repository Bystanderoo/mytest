## 剑指offer48.最长不含重复字符的子字符串

原题：https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

```c
示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```


提示：

```
s.length <= 40000
```

思路解析：

数组+滑动窗口

比较难想的点是数组里存的是左节点下一跳地址

```c
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> m(128, 0);
        int ans = 0;
        int i = 0;
        for (int j = 0; j < s.size(); j++) {
            i = max(i, m[s[j]]);//如果有重复则跳到下个重复的字符的下个位置
            m[s[j]] = j + 1;//记录重复时应去的位子
            ans = max(ans, j - i + 1);
        }
        return ans;
    }
};
```



方法二：

hashmap，但是是暴力解法，运行时间长，消耗内存也多

```c
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        //只打败了5%
        unordered_map<char,int> hashmap;
        int max=0;
        int count=0;
        for(int i=0;i<s.size();i++){
            auto it = hashmap.find(s[i]);
            if(it!=hashmap.end()){
                //重复
                if(count>max){
                    max=count;
                }
                i=i-count;
                hashmap.clear();
                count=0;
            }else{
                hashmap[s[i]]=i;
                count++;
            }
        }
        if(count>max) max=count;
        return max;
    }
}
```

