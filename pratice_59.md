#### 59. 螺旋矩阵 II
题意：给定一个正整数 n，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

解题思路：模拟题，比较简单，从外往里，按照规则填数就行

1A 0ms

```
func generateMatrix(n int) [][]int {
	count := n * n
	var result [][]int
	for i := 0 ; i < n; i++{
		temp := make([]int,n)
		result = append(result,temp)
	}
	left, right, top, bottom := 0, n-1, 0, n-1
	num := 1
	for{
		for i := left; i <= right; i++ {
			result[top][i] = num
			num++
		}
		if num > count {
			break
		}
		top++
		for i := top; i <= bottom; i++ {
			result[i][right] = num
			num++
		}
		if num > count {
			break
		}
		right--
		for i := right; i >= left; i-- {
			result[bottom][i] = num
			num++
		}
		if num > count {
			break
		}
		bottom--
		for i := bottom; i >= top; i-- {
			result[i][left] = num
			num++
		}
		if num > count {
			break
		}
		left++

	}
	return result
}

```