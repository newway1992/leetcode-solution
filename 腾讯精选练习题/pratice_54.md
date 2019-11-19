#### 54. 螺旋矩阵
题意：给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

解题思路：模拟题，跟剥洋葱一样，从外往里，每次遍历一行或者一列修改left，right，top，bottom值就行

1A 0ms

```
func spiralOrder(matrix [][]int) []int {
	m := len(matrix)
	n := 0
	if m > 0 {
		n = len(matrix[0])
	}
	//fmt.Printf("m * n = %d * %d", m, n)
	result := make([]int, 0)
	left, right, top, bottom := 0, n-1, 0, m-1
	count := m * n
	for {
		for i := left; i <= right; i++ {
			result = append(result, matrix[top][i])
		}
		if len(result) >= count {
			break
		}
		top++
		for i := top; i <= bottom; i++ {
			result = append(result, matrix[i][right])
		}
		if len(result) >= count {
			break
		}
		right--
		for i := right; i >= left; i-- {
			result = append(result, matrix[bottom][i])
		}
		if len(result) >= count {
			break
		}
		bottom--
		for i := bottom; i >= top; i-- {
			result = append(result, matrix[i][left])
		}
		if len(result) >= count {
			break
		}
		left++
	}
	return result
}

```