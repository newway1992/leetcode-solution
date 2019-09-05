### 6.Z字形变换

解题思路：模拟题，构建一个m*n的二维数组，将字符按规则填入然后输出
1A 192ms 这个时间比较感人，代码就不列出来了

提交完发现，其实只要确定各字符在哪一行，然后把每行字符按序输出就行了，字符只有两种走向，一种竖直，一种折线，每次到第一行或者最后一行时改变走向，优化后重新提交。
1A 4ms 这才是golang的正确姿势
```
func convert(s string, numRows int) string {
	if numRows == 1 {
		return s
	}
	result := make([]string, 0)
	for i := 0; i < numRows; i++ {
		result = append(result, "")
	}
	count := len(s)
	i, j := 0, 0
	index := 0
	//是否竖直走向
	isVertical := true
	for index < count {
		//fmt.Printf("i:%d j:%d v:%c index:%d\n", i, j, s[index], index)
		if isVertical {
			result[j] += string(s[index])
			j++
			index++
			if j == numRows-1 {
				isVertical = false
			}
		} else {
			result[j] += string(s[index])
			i++
			j--
			index++
			if j == 0 {
				isVertical = true
			}
		}
	}
	validStr := ""
	for i := 0; i < numRows; i++ {
		validStr += result[i]
	}
	return validStr
}
```