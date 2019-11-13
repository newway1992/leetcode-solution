#### 62. 不同路径
题意：给定m * n格子，求从(0,0)到(m - 1,n -1)有多少条不同路径，规定每次只能向右或者向下移动

解题思路：典型dp问题，由于每次只能向右或者向下移动，那么对于某个格子(i,j),到达它的路径条数就等于左边格子和上边格子之和，dp[i][j] = dp[i - 1][j] + dp[i][j - 1](当i>1 && j>1时)，初始化时将第一行和第一列置为1

1A 12ms

```
func maxArea(height []int) int {
	maxArea := 0
	count := len(height)
	i, j := 0, count-1
	for i < j {
		area := (j - i) * int(math.Min(float64(height[i]), float64(height[j])))
		if area > maxArea {
			maxArea = area
		}
		if height[i] < height[j] {
			i++
		} else {
			j--
		}
	}
	return maxArea
}
```