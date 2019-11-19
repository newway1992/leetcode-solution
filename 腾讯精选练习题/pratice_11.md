#### 11.盛最多水的容器
题意：给定N条线段，求构成的最小矩形面积

解题思路：数据比较水，暴力破解都能过。当然还是推荐o(n)方法，当底边一定时，矩形的面积是由最短线段决定的，从左右两端同时开始扫描，对于左端，如果后面的线段比前面的线段短，那么构成矩形面积一定比之前的要小，同理，对于右端，如果前面的线段比后面的线段短，构成的矩形面积也要小，不满足条件的线段过滤掉，然后计算满足条件的线段构成的最大矩形面积

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