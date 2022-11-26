- [11月24日](#11月24日)
  - [两数之和\[简单\]](#两数之和简单)
    - [题解](#题解)
# week 1
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
           mp.insert(pair<int, int>(nums[i], i));//等价于mp[nums[i]] = i;
       }
       return {};
    }
};
```

#### 题解

1. 主要通过unordered_map的find()函数来降低时间复杂度：哈希查找只需要O(1)复杂度。
2. 每次查找都从当前节点nums[i]查找之前的元素nums[0]~nusm[i-1]有没有等于target - nums[i]的。
3. map(key, value)结构，在key位置放入nums[i]，在value位置放入i，因为哈希查找是根据唯一的key去查找value，对应根据num[i]去查找下标i。

## 11.25

## 11.26
### 移动零[简单]
1. 双指针法——两次循环，时间复杂度O(N)
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        //双指针法
        int j = 0; //指针j指向将要被赋值的不为0元素，放在循环外，用于记录j最后的位置
        for (int i = 0; i < nums.size(); i++) {
            //指针i扫描整个数组
            if (nums[i] != 0) {
                //当前扫描到的元素不为0，那么赋值给nums[j]，并且j++
                nums[j++] = nums[i];
            }
            //如果nums[i] == 0，不仅不会复制给nums[j]，而且j不会自增，但是i++
            //由此做到nums[j]只接受不为0的元素
        }
        //j指向下一个待赋值的位置，但是i已经扫描完了所有不为0的元素。
        //接下来的全赋值为0即可
        for (int i = j; i < nums.size(); i++) {
            nums[i] = 0;
        }
    }
};
```
2. 双指针法——一次循环，时间复杂度O(N)
3. ```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        //双指针法
        int j = 0; //指针j指向将要被赋值的不为0元素，放在循环外，用于记录j最后的位置
        for (int i = 0; i < nums.size(); i++) {
            //指针i扫描整个数组
            if (nums[i] != 0) {
                //当前扫描到的元素不为0，那么赋值给nums[j]，并且j++
                nums[j] = nums[i];//不能nums[j++] = nums[i]; 因为下一步必定 i != j
                if (i != j) {
                    nums[i] = 0;//i != j 说明i已经已经到了j的前面，在已经赋值给nums[j]后
                    //再将自己置为0，可以保证在一遍扫描结束后末尾元素[j + 1, nums.size() - 1]全为0；
                }
                j++;
            }
            //如果nums[i] == 0，不仅不会复制给nums[j]，而且j不会自增，但是i++
            //由此做到nums[j]只接受不为0的元素
        }
        // //j指向下一个待赋值的位置，但是i已经扫描完了所有不为0的元素。
        // //接下来的全赋值为0即可
        // for (int i = j; i < nums.size(); i++) {
        //     nums[i] = 0;
        // }
    }
};
```
3. 双指针法——一次循环，去除重复赋值，时间复杂度O(N)
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int j = 0; 
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != 0) {
                if (i != j) {
                    nums[j] = nums[i];//只有当 i > j 时才需要赋值。
                    nums[i] = 0;
                }
                j++;
            }
        }
    }
};
```
