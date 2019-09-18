#### 16.最接近的三数之和
题意：给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

解题思路：

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