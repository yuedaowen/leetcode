## leetcode Q1#1-Two Sum

### **0x01 我的解法**
需要简单的数组知识，暴力搜索即可AC

### **0x02 代码参考**

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        vector<int> result;
        for(int i = 0; i < n; i++){
        for(int j = i + 1; j < n; j++){
            if(nums[i] + nums[j] == target){
                result.push_back(i);
                result.push_back(j);
                break;
            }
        }
    }
        return result;
    }
};
```
### **0x03 反思总结**

本题我使用了暴力搜索方法，时间复杂度为O(n^2),这在大多数情况下可能不会AC。
使用Hash表，以空间换时间，可以让时间复杂度将为O(n)，但同时空间复杂度也升为O(n)。

并且，采用hash表的情况下，有两次遍历解决问题的情况，也有一次遍历解决问题的情况。

---

## leetcode Q2#7-Reverse Integer

### **0x01 我的解法**

将给定的数x逐次对10的m(0~k)整除及余除，分别得到每个十进制位上的位数，然后再反向构造出reverse过后的整数

溢出判断

* 如果reverse操作后得到的数位数达到10位，且最高位大于2，则一定溢出
* 其他情况，由于最终结果是由 `ans = ans + res[i] * pows[i]` ，适用于两个数相加减判断溢出的情况

### **代码参考**

```C++
class Solution {
public:
    int reverse(int x) {
        if(x == 0) return 0;
        int pows[] ={1,10,100,1000,10000,100000,1000000,10000000,100000000,1000000000};
        int m = 9;
        int flag = x / pows[m];
        int res[10] = {0};
        while(!flag){
            m --;
            flag = x / pows[m];
        }
        int num = m;
        // m + 1 是n的位数
        int ans = 0; //存储结果
        int temp = x;
        for(int i = 0; m >= 0; m--,i++){
            res[i] = temp / pows[m];
            temp = temp % pows[m];
        }
        if(num == 9 && res[9] > 2) return 0;
        for(int i = num; i >= 0; i--){
            ans += res[i] * pows[i];
        }
        if((x > 0 && ans > 0) || (x < 0 && ans < 0)) return ans;
        return 0;
    }
};
```

### **反思总结**

本题的关键是溢出判断，可以适当记忆一些常见的数据类型表示范围，比如本题中`32bit int`表示范围为`(–2147483647 – 1,2147483647)`。

另外，不使用字符串处理函数的情况下，单独取出十进制数每一位的方法值得注意，包含顺序取出，逆序取出

***

## leetcode Q3#26-Remove Duplicates from Sorted Array

### **0x01 我的解法**

看到本题，第一直觉，想到在一次遍历数组的时候，用一个`Hash`表记录已经出现的数，同时这个`Hash`表用于判重，`i`与`j`分别作为赋值指针与游标向后移动，直到`j`遍历到最后一个元素结束。


### **代码参考**

```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        map<int,int> flag;
        int s = nums.size();
        int i,j;
        for(i = 0,j = 0; j < s;){
            while(flag.find(nums[j++]) != flag.end() && j <= s);
            if(j <= s){
                nums[i] = nums[j-1];
                flag[nums[i]] = 1;
                i++;
            }
            while(1);
        }
        return i;
    }
};
```

### **反思总结**

我自己的解法确实可行，用C++ STL库的`map`表代替`Hash`表实现，但是，题目中**明明已经说明给定的数组是有序数组**，所以完全用不着`Hash`，直接使用双指针法就可以。

另外，在处理`while`与`for`循环的边界问题时总是容易出错，需要加强练习。