#### 15.三数之和
题意：从给定数组中挑选出三个数的组合，满足a+b+c=0，注意去重

解题思路：暴力方法O(n^3)，应该会超时，没有尝试，这里是o(n^2)的解法，把数组从小到大排序,然后拆分为负数数组和正数数组(去重处理)，0单独考虑，且用一个map记录每个数值的出现次数
满足条件的组合有一下四种情况:

1. 3个0(查看map记录0的个数)
2. 1个0 一正一负(遍历正数数组，看相反数在map是否存在)
3. 两正一负(双重for循环正数数组，两数之和取相反数看map中是否存在)
4. 两负一正(双重for循环负数数组，两数之和取相反数看map中是否存在)

开始未处理3个0的情况WA了一次 后来修正AC 1336ms

```
func threeSum(nums []int) [][]int {
	result := make([][]int, 0)
	sort.Ints(nums)
	postiveNums := make([]int, 0)
	negativeNums := make([]int, 0)
	var storage map[int]int
	storage = make(map[int]int)
	for i := 0; i < len(nums); i++ {
		if storage[nums[i]] == 0 {
			if nums[i] > 0 {
				postiveNums = append(postiveNums, nums[i])
			}
			if nums[i] < 0 {
				negativeNums = append(negativeNums, nums[i])
			}
		}
		storage[nums[i]]++
	}
	sort.Ints(postiveNums)
	sort.Ints(negativeNums)
	//fmt.Println(postiveNums)
	//fmt.Println(negativeNums)
	//1.3个0
	if storage[0] >= 3 {
		temp := make([]int, 0)
		temp = append(temp, 0, 0, 0)
		result = append(result, temp)
	}
	//2.一正一负一0
	if storage[0] >= 1 {
		for i := 0; i < len(postiveNums); i++ {
			temp := make([]int, 0)
			a, b := postiveNums[i], 0
			c := -a - b
			if storage[c] > 0 {
				temp = append(temp, a, b, c)
				sort.Ints(temp)
				result = append(result, temp)
			}
		}
	}
	//3.两正一负
	for i := 0; i < len(postiveNums); i++ {
		for j := i; j < len(postiveNums); j++ {
			a,b := postiveNums[i],postiveNums[j]
			if a == b{
				if storage[a] < 2{
					continue
				}
			}
			c := -a - b
			if storage[c] > 0{
				temp := make([]int,0)
				temp = append(temp,a,b,c)
				sort.Ints(temp)
				result = append(result,temp)
			}
		}
	}
	//4.两负一正
	for i := 0; i < len(negativeNums); i++ {
		for j := i; j < len(negativeNums); j++ {
			a,b := negativeNums[i],negativeNums[j]
			if a == b{
				if storage[a] < 2{
					continue
				}
			}
			c := -a - b
			if storage[c] > 0{
				temp := make([]int,0)
				temp = append(temp,a,b,c)
				sort.Ints(temp)
				result = append(result,temp)
			}
		}
	}
	return result
}
```