### 剑指offer 45.把数组排成最小的数

原题链接：[https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/]()

![image-20210419202458032](C:\Users\ZFJ\AppData\Roaming\Typora\typora-user-images\image-20210419202458032.png)

归根结底是一个排序问题，只不过这个排序和普通的排序不同，应该根据组合后数的大小来确定“小”还是“大”，（x、y都是string类型）如果x+y>y+x  ，则说明x>y。

##### 方法一

重写快速排序

```c++
class Solution {
public:
// 快排序修改
    void quickSort(vector<int>& nums,int l,int r){
        if(l<r){
            int i=l,j=r;
            int myX=nums[l];
            string X=to_string(nums[l]);
            while(i<j){
                while(i<j&&X+to_string(nums[j])<=to_string(nums[j])+X){
                    j--;
                }
                if(i<j){
                    nums[i]=nums[j];
                }
                while(i<j&&X+to_string(nums[i])>to_string(nums[i])+X){
                    i++;
                }
                if(i<j){
                    nums[j]=nums[i];
                }
            }
            nums[i]=myX;
            quickSort(nums,l,i-1);
            quickSort(nums,i+1,r);
        }
    }
    string minNumber(vector<int>& nums) {
        //第一个可以为0，数不可拆，第一位小的在前面
        //排序 x+y>y+x  即y<x 快速排序
        string res="";
        int len = nums.size();
        quickSort(nums,0,len-1);
        for(int i=0;i<len;i++){
            res+=to_string(nums[i]);
        }
        return res;
    }
};
```

##### 方法二

对内置排序函数进行规则重订

```c++
class Solution {
public:
    //这个函数必须是static
	static bool cmp(string &x,string &y){
        return x+y<y+x;
    }
    string minNumber(vector<int>& nums) {
        string res="";
        vector<string> mynum;
        for(int i=0;i<nums.size();i++){
            mynum.push_back(to_string(nums[i]));
        }
        sort(mynum.begin(),mynum.end(),cmp);
        //sort(mynum.begin(),mynum.end(), [](string& x, string& y){ return x + y < y + x; });
        for(int i=0;i<mynum.size();i++){
            res+=mynum[i];
        }
        return res;
    }
}
```

##### 加一些关于C++比较细碎的点：

###### -数类型的转换

1. int -> string       to_string(x)

```c++
int x = 10;
string str;
str = to_string(x);
```

2.  string -> char    str.c_str()

```c++
//对于char*   c_str()方法
string str = "123";
const char* a;
a = str.c_str();

//对于char[]  copy()方法
string str1 = "345";
char b[20];
str1.copy(b,str1.size(),0);//0表示从第0位开始复制
*(b+str1.size())='\0';
```

3.  string -> int        atoi(char *)

   string -> float     atoi(char *)

   ```c++
   string str = "303";
   int x = atoi(str.c_str());
   
   string str1 = "303.33";
   float y = atof(str1.c_str());
   ```

3. int ->float       (float) x

   int ->double   (double) x

   double -> int  (int) d

   float -> int      (int) f