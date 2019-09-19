#### 16.最接近的三数之和
题意：给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

解题思路：双指针解法，将数组从小到大排列，遍历数组，选中nums[i]，双指针left和right分别为i+1，len(nums) - 1，令sum = nums[i] + nums[left] + nums[right]，因为sum要趋近于target，所以sum偏小时，left向左移动，sum偏大时，right向右移动，如果出现sum == target，此时最接近，直接返回，否则将差值和diff比较并刷新diff。

4ms

```
func threeSumClosest(nums []int, target int) int {
	sort.Ints(nums)
	count := len(nums)
	result := 0
	diff := math.MaxFloat64
	for i := 0; i < count - 2; i++ {
		a := nums[i]
		//去重
		if i > 0 && a == nums[i-1] {
			continue
		}
		left := i + 1
		right := count - 1
		for left < right{
			sum := a + nums[left] + nums[right]
			if sum == target{
				return target
			}else{
				if math.Abs(float64(sum - target)) < diff{
					diff = math.Abs(float64(sum - target))
					result = sum
				}
				if sum < target{
					left++
				}else if sum > target{
					right--
				}
			}
		}

	}
	return result
}
```