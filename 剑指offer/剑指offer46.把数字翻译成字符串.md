## 剑指offer46.把数字翻译成字符串

原题链接 https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

```C
示例 1:

输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

提示：

0 <= num < 2^31

解题思路：这种题肯定不是直接遍历，是找规律题，找到规律后，可以直接写也可以递归。

f(n)=f(n-1)+f(n-2)

方法一：

一开始的思路：

整体比较麻烦的是三个判断条件，前一个不能为0这个很难想到。

```c
class Solution {
public:
    int translateNum(int num) {
        vector<int> mynum;
        while(num!=0){
            mynum.push_back(num%10);
            num=num/10;
        }
        mynum.push_back(0);
        reverse(mynum.begin(),mynum.end());
        int len=mynum.size();
        vector<int> myvector(len+1,0);
        myvector[0]=1;
        myvector[1]=1;
        for(int i=2;i<len;i++){
            if((mynum[i-1]>2)||(mynum[i-1]==2&&mynum[i]>5)||mynum[i-1]==0){
                myvector[i]=myvector[i-1];
            }else{
                myvector[i]=myvector[i-1]+myvector[i-2];
            }
        }

        return myvector[len-1];
    }
};
```

写完看了一下解题，解题是直接使用to_string()函数将int转为string，就不需要像上面一样转成vector后还要转置。

优化如下：比上面内存消耗小一些。

```
注意：
用string类型要注意每一个存的是char，需要减掉'0'。
循环由于上面有再 vector 的 mynum 前加了个0，改成string后没有加，所以循环条件有所改变。
```

```C
class Solution {
public:
    int translateNum(int num) {
        string mynum = to_string(num);
        int len=mynum.size();
        vector<int> myvector(len+1,0);
        myvector[0]=1;
        myvector[1]=1;
        for(int i=2;i<=len;i++){
            int temp1=mynum[i-2]-'0';
            int temp2=mynum[i-1]-'0';
            if((temp1>2)||(temp1==2&&temp2>5)||temp1==0){
                myvector[i]=myvector[i-1];
            }else{
                myvector[i]=myvector[i-1]+myvector[i-2];
            }
        }
        return myvector[len];
    }
};
```

方法二：递归

从提交里拷贝了一份内存消耗最小的代码。如下：

```c
//递归解法，从左往右统计，先求出当前位的可能，再递归剩余位的可能
class Solution {
public:
    int translateNum(int num) {
        string data = to_string(num);
        return translateNumCore(data,0);
    }

    int translateNumCore(string data, int index)
    {
        int length = data.size();
        if (length == 0)
            return 0;
        if (index >= length - 1)
            return 1;
        if(data[index]>'2'|| data[index]=='0'||(data[index] == '2' && data[index + 1] > '5'))
            return  translateNumCore(data, index+1);
        else
        {
            return  translateNumCore(data, index + 1)+ translateNumCore(data, index + 2);
        }
    }
};
```

