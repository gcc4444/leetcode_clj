## 11月24日
### 两数之和[简单]
**1. O(N<sup>2</sup>)时间复杂度**
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> res;
        for (int i = 0; i < nums.size() - 1; i++) {
            for (int j = i + 1; j < nums.size(); j++ ) {
                if (nums[i] + nums[j] == target) {
                    res.push_back(i), res.push_back(j);
                    return res;
                }
            }
        }
        return res;
    }
};
```
**2.O(N)复杂度**
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
       unordered_map<int, int> mp;
       for (int i = 0; i < nums.size(); i++) {
           auto it = mp.find(target - nums[i]);
           if (it != mp.end()) {
               return {i, it->second};
           }
           mp.insert(pair<int, int>(nums[i], i));
       }
       return {};
    }
};
```

#### 题解

1. 主要通过unordered_map的find()函数来降低时间复杂度：哈希查找只需要O(1)复杂度。
2. 每次查找都从当前节点nums[i]查找之前的元素nums[0]~nusm[i-1]有没有等于target - nums[i]的。
3. map(key, value)结构，在key位置放入nums[i]，在value位置放入i，因为哈希查找是根据唯一的key去查找value，对应根据num[i]去查找下标i。
