## leetcode Q1

### **0x01 基本信息**
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