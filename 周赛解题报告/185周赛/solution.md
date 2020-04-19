5388  
https://leetcode-cn.com/problems/reformat-the-string/  

按要求生成字符串，要求字母数字必须间隔，所以给定字符串中字母数量和数字数量差的绝对值必须小于等于1
```
func reformat(s string) string {
	ans := ""
	numArr := make([]string,0)
	chaArr := make([]string,0)
	for _,v := range s{
		if v >= 97 && v <= 122{
			chaArr = append(chaArr,string(v))
		}else{
			numArr = append(numArr,string(v))
		}
	}
	fmt.Println(chaArr)
	fmt.Println(numArr)
	if math.Abs(float64(len(chaArr) - len(numArr))) > 1{
		return ""
	}else{
		if len(chaArr) > len(numArr){
			for i := 0; i < len(numArr); i++{
				ans += chaArr[i]
				ans += numArr[i]
			}
			ans += chaArr[len(chaArr) - 1]
		}else if len(chaArr) < len(numArr){
			for i := 0; i < len(chaArr); i++{
				ans += numArr[i]
				ans += chaArr[i]
			}
			ans += numArr[len(numArr) - 1]
		}else{
			for i := 0; i < len(chaArr); i++{
				ans += chaArr[i]
				ans += numArr[i]
			}
		}
	}
	return ans
}
```  

5389  
https://leetcode-cn.com/problems/display-table-of-food-orders-in-a-restaurant/  

生成菜单，题目很长，理解题意就行，注意桌子序号和菜名要按字典序排列  
```
func displayTable(orders [][]string) [][]string {
	ans := make([][]string,0)
	stat := make(map[int]map[string]int)
	for i := 0; i < len(orders); i++{
		tableId,_ := strconv.Atoi(orders[i][1])
		foodName := orders[i][2]
		if stat[tableId] == nil{
			stat[tableId] = make(map[string]int)
		}
		stat[tableId][foodName]++
		//fmt.Printf("%d %s %d\n",tableId,foodName,stat[tableId][foodName])
	}
	//table sort
	tableIds := make([]int,0)
	nameKeys := make([]string,0)
	nameSet := make(map[string]bool)
	for k,v := range stat{
		tableIds = append(tableIds,k)
		for foodName,_ := range v{
			if !nameSet[foodName]{
				nameKeys = append(nameKeys,foodName)
				nameSet[foodName] = true
			}
		}
	}
	sort.Ints(tableIds)
	sort.Strings(nameKeys)
	titleStr := make([]string,0)
	titleStr = append(titleStr,"Table")
	for i := 0; i < len(nameKeys); i++{
		titleStr = append(titleStr,nameKeys[i])
	}
	ans = append(ans,titleStr)
	for i := 0; i < len(tableIds); i++{
		tempStr := make([]string,0)
		tempStr = append(tempStr,strconv.Itoa(tableIds[i]))
		for j := 0; j < len(nameKeys); j++{
			tempStr = append(tempStr,strconv.Itoa(stat[tableIds[i]][nameKeys[j]]))
		}
		ans = append(ans,tempStr)
	}
	//fmt.Println(stat)
	return ans
}
```
5390  
https://leetcode-cn.com/problems/minimum-number-of-frogs-croaking/  

给定字符串中"c","r","o","a","k"数量必定相等，遍历一次，分别记录对应字符的数量，注意后面的字符不能超过前面的字符数量，找到一个“croak”就将相应字符数量减1，最后所有字符数量等于0则满足条件，且中间出现的字符c最大值即为最少青蛙的个数
```
func minNumberOfFrogs(croakOfFrogs string) int {
	ans := -1
	stat := make(map[string]int)
	for i := 0; i < len(croakOfFrogs); i++{
		stat[string(croakOfFrogs[i])]++
		if stat[string(croakOfFrogs[i])] >= ans{
			ans = stat[string(croakOfFrogs[i])]
		}
		if stat["c"] < stat["r"] ||  stat["c"] < stat["o"] ||  stat["c"] < stat["a"] ||  stat["c"] < stat["k"]{
			break
		}
		if stat["r"] < stat["o"] ||  stat["r"] < stat["a"] ||  stat["r"] < stat["k"]{
			break
		}
		if stat["o"] < stat["a"] ||  stat["o"] < stat["k"]{
			break
		}
		if stat["a"] < stat["k"]{
			break
		}
		if stat["c"] >= 1 && stat["r"] >= 1 && stat["o"] >= 1 && stat["a"] >= 1 && stat["k"] >= 1{
			stat["c"]--
			stat["r"]--
			stat["o"]--
			stat["a"]--
			stat["k"]--
		}
	}
	if stat["c"] == 0 && stat["r"] == 0 && stat["o"] == 0 && stat["a"] == 0 && stat["k"] == 0{
		return ans
	}
	return -1
}
```

5391  
https://leetcode-cn.com/problems/build-array-where-you-can-find-the-maximum-exactly-k-comparisons/  
比赛时没做出来，每次hard被卡，讨论圈看到有人说把周赛hard题刷一遍就差不多了，找个机会试试  


