#### 18.四数之和
题意：给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。
注意：
答案中不可以包含重复的四元组。

解题思路：双指针解法，将数组从小到大排列，双重for循环，固定nums[i]和nums[j]，双指针left和right分别为j+1，len(nums) - 1，令sum = nums[i] + nums[j] + nums[left] + nums[right]，因为sum要等于target，所以sum偏小时，left向左移动，sum偏大时，right向右移动，如果出现sum == target，存储该四元组组合。

24ms 1A 加上剪枝优化后 4ms

```
func fourSum(nums []int, target int) [][]int {
	count := len(nums)
	sort.Ints(nums)
	result := make([][]int, 0)
	for i := 0; i < count-3; i++ {
		//去重
		if i > 0 && nums[i] == nums[i-1] {
			continue
		}
		//此时最小的sum都大于target，后面就不用查询了
		if nums[i]+nums[i+1]+nums[i+2]+nums[i+3] > target {
			break
		}
		//nums[i]固定，最大的sum小于target，增大nums[i]继续查询
		if nums[i]+nums[count-3]+nums[count-2]+nums[count-1] < target {
			continue
		}
		for j := i + 1; j < count-2; j++ {
			//去重
			if j > i+1 && nums[j] == nums[j-1] {
				continue
			}
			//此时最小的sum都大于target，后面就不用查询了
			if nums[i]+nums[j]+nums[j+1]+nums[j+2] > target {
				break
			}
			//nums[i]和nums[j]固定，最大的sum小于target，增大nums[j]继续查询
			if nums[i]+nums[j]+nums[count-2]+nums[count-1] < target {
				continue
			}
			left, right := j+1, count-1
			for left < right {
				//去重
				if left > j+1 && nums[left] == nums[left-1] {
					left++
					continue
				}
				//去重
				if right < count-1 && nums[right] == nums[right+1] {
					right--
					continue
				}
				sum := nums[i] + nums[j] + nums[left] + nums[right]
				if sum == target {
					temp := make([]int, 0)
					temp = append(temp, nums[i], nums[j], nums[left], nums[right])
					result = append(result, temp)
					left++
					right--
				} else if sum < target {
					left++
				} else if sum > target {
					right--
				}
			}
		}
	}
	return result
}
```