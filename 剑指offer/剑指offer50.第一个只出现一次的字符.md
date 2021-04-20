## 剑指offer50.第一个只出现一次的字符

原题链接 https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

示例:

```c
s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
```

限制：

0 <= s 的长度 <= 50000

思路解析：

首先要存储字母出现的次数，其次要保存第一个只出现一次的字符

方法一：

数组+队列

```c
class Solution {
public:
    char firstUniqChar(string s) {
        vector<int> myvector(128,0);
        queue<char> myqueue;
        for(int i=0;i<s.size();i++){
            char temp=s[i];
            myvector[temp]++;
            if(myvector[temp]==1){
                myqueue.push(temp);
            }else if(myvector[temp]>1){
                if(temp==myqueue.front()){
                    myqueue.pop();
                }
            }
        }
        //防止意外发生，例如一个出现一次，后面都是一次以上，一次pop出之后，后续就是两次，所以需要多加一次保障。
        while(!myqueue.empty()&&myvector[myqueue.front()]>1){
            myqueue.pop();
        }
        if(myqueue.empty()){
            return ' ';
        }
        return myqueue.front();
    }
};
```

方法二：

一个数组，遍历两次。这是看了解析才知道的。

```c
class Solution {
public:
	char firstUniqChar(string s) {
        vector<int> myvector(128,0);
        for(char c : s){
            myvector[c]++;
        }
        for(char c : s){
            if(myvector[c]==1){
                return c;
            }
        }
        return ' ';
    }
};
```

