## Money Robbing
### 线性排列
#### algorithm
```
Input: 列表v
Output: 最大抢劫金额
1. 初始化一个一维数组f
2. for i in range(2,len(v)+2):
	1. f[i] = max(f[i-1],f[i-2]+v[i-2])
3. return f[len(v)+1]
```
#### optimal substructure
```
f[i] = max(f[i-1],f[i-2]+v[i])
```
#### correctness
所有的结点都是正值，因此当劫匪到达某一节点时候，只会在上一个节点行窃与上上个节点行窃两种可能，此时劫匪可以选择在该节点行窃，或者不再该节点行窃，对应了最优子结构。
例如对于输入数据：1,2,3,4,5
f[0] = 0，padding位
f[1] = 0，padding位
f[2] = max(f[1],f[0]+v[1]) = 1，在1号行窃
f[3] = max(f[2],f[1]+v[2]) = 2，在2号行窃
f[4] = max(f[3],f[2]+v[3]) = 4，在1，3行窃
f[5] = max(f[4],f[3]+v[4]) = 6，在2，4行窃
f[6] = max(f[5],f[4]+v[5]) = 9，在1，3，5行窃
f[6]是最大化的行窃收益。
#### complexity
不考虑初始化成本。主体为一个for循环，循环体内部为一个加法和三个取值，可记为O(1)，故而总体的时间复杂度是O(n).

### 环形结构
#### algorithm
```
Input: 列表v
Output: 最大抢劫金额
1. 初始化两个个一维数组f1,f2
2. for i in range(2,len(v)+1):
	1. f1[i] = max(f1[i-1],f1[i-2]+v[i-2])
3. for i in range(3,len(v)+2):
	1. f2[i] = max(f2[i-1],f2[i-2]+v[i-2])
4. return max(f1[-1],f2[-1])
```
#### optimal substructure
与上一问相同。
```
f[i] = max(f[i-1],f[i-2]+v[i])
```
#### correctness
当节点是一个环时，第一个节点和最后一个节点只能取一个，所以拆分为两个线性结构问题去做即可。
例如对于输入数据：1,2,3,4,5 (环形)
第一个子问题，1,2,3,4
f[0] = 0，padding位
f[1] = 0，padding位
f[2] = max(f[1],f[0]+v[1]) = 1，在1号行窃
f[3] = max(f[2],f[1]+v[2]) = 2，在2号行窃
f[4] = max(f[3],f[2]+v[3]) = 4，在1，3行窃
f[5] = max(f[4],f[3]+v[4]) = 6，在2，4行窃
第二个子问题，2,3,4,5
f[0] = 0，padding位
f[1] = 0，padding位
f[2] = max(f[1],f[0]+v[1]) = 2，在1号行窃
f[3] = max(f[2],f[1]+v[2]) = 3，在2号行窃
f[4] = max(f[3],f[2]+v[3]) = 6，在1，3行窃
f[5] = max(f[4],f[3]+v[4]) = 8，在2，4行窃
子问题合并，max(f1,f2) = max(6,8) = 8.
#### complexity
相当于执行了两次第一问的算法，故而复杂度为2O(n)，省去常数还是为O(n).
## Ugly Number
### 第一问
#### algorithm
```
Input: n
Output 第n个丑数 (默认1是第一个)
1. f = []
2. f[1] = 1
3. idx = 1
4. while(idx<n):
	1. backup = []
	2. backup += [2*i for i in f] # 将f中所有元素乘2添加到backup中
	3. backup += [3*i for i in f]
	4. backup += [5*i for i in f]
	5. f[idx++] = min(backup)
6. return f[n]
```
#### correctness
后面的丑数可以由于前面的丑数乘上2,3,5得到，为了获得最小的就将所有的已知的乘上2,3,5然后取最小。
#### complexity
外层循环n次，内层在线性表取最小O(n)复杂度，故而总计需要O(n^2).
### 第二问
#### algorithm
```
Input: n
Output 第n个丑数 (默认1是第一个)
1. f = []
2. f[1] = 1
3. p1,p2,p3 = 1,1,1
4. idx = 1
5. while(idx<n):
	1. t = min(f[p1]*2,f[p2]*3,f[p3]*5)
	2. f[idx++] = t
	3. if t == f[p1]*2:
		1. p1++
	4. if t == f[p2]*3:
		1. p2++
	5. if t == f[p3]*3:
		1. p3++
6. return f[n]
```
#### optimal structure
f[i] = min(f[p1]\*2,f[p2]\*3,f[p3]\*5)
#### correctness
1是最小的丑数。丑数是2，3，5的倍数，因此用已知丑数乘上2，3，5取最小值即可获得下一个丑数。通常来说可能需要一个比较大小的过程，但是使用三个指针可以优化这一过程。三个指针所指向的元素分别乘上2，3，5再比较大小，最小的那个就向前移动一个元素，这样每次只需要比较三个元素的大小。
#### complexity
while循环n次，内层每次比较3个数字大小，然后指针移动，总的时间复杂度是O(n).
## Unique Binary Search Trees
#### algorithm
```
Input: n
Ouput: unique BST's number
1. 初始化一个二维数组f
2. f[0] = 1
4. for i in range(1,n+1):
	1. f[i] = 0
	2. for j in range(0,i+1):
		1. f[i] += f[j]*f[i-1-j]
5. return f[n]
```
#### optimal structure
见下一小节。
#### correctness 
令f[i,n]表示以i为根节点，长度为n的二叉搜索树数量。
G[n]表示长度为n的二叉搜索树数量。
当根节点i确定后，其左侧子树的数量有G[i-1]个，其右侧子树的数量为G[n-i]个，
故而有f[i,n] = G[i-1] \* G[n-i]，
同时，G[n] = sum( f[i, n]).
#### complexity
两层循环，外层循环n次，内层循环1,2,3,4...n次，共计时间复杂度为O(n^2).
## Largest Divisible Subset
#### algorithm
```
Input: 数组v
Output: 最大子集size
1. v = sort(v) # 先从小到大排序
2. 初始化二维数组f
3. for i in range(0, len(v)):
	1. for j in range(0,i):
		1. for k in range(0,j):
			1. if v[j] mod v[k] == 0:
				1. f[i,j] = max(f[i-1,k]+1)
4. ret = 0
5. for i in range(0,len(v)):
	1. ret = max(ret, f[len(v)-1, i])
6. return ret
```
#### optimal structure
f[i,j] = max(f[ i-1,k ] + 1) (其中 v[j] mod v[k]=0)
#### correctness 
因为要找整除子集，那么不妨先将整个数组从小到大排序，这样就可以标记整除集合中最后一个元素的位置。
f[i,j]表示的是前i个数字中，以j结尾的整除集的长度。
例如输入的数据为1,2,3,4,5,6,7,8
则状态转移表为：

|     | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 1   |     |     |     |     |     |     |     |
| 2   | 1   | 2   |     |     |     |     |     |     |
| 3   | 1   | 2   | 2   |     |     |     |     |     |
| 4   | 1   | 2   | 2   | 3   |     |     |     |     |
| 5   | 1   | 2   | 2   | 3   | 2   |     |     |     |
| 6   | 1   | 2   | 2   | 3   | 2   | 3   |     |     |
| 7   | 1   | 2   | 2   | 3   | 2   | 3   | 2   |     |
| 8   | 1   | 2   | 2   | 3   | 2   | 3   | 2   | 4   | 
只需要将最后一行取一个max即可。
#### complexity
三层循环，每层循环的执行次数都是O(n)，最后在线性表中取max花费O(n)，时间复杂度为O(n^3)+O(n)，即O(n^3).
## Target Sum
#### algorithm
```
Input: 数组nums, 目标target
Ouput: 不同的添加符号方案数量
1. 初始化一个二维数组f # 数组下标本不应该为负，这里为了简化，允许其为负数，真实代码中应采用偏移值。
2. high = sum(nums)
3. low = -high
4. f[0,nums[0]] = 1
5. f[0,-nums[0]] = 1
6. for i in range(1, len(nums)):
	for j in (low, high):
		f[i,j] = f[i-1,j-nums[i]] + f[i-1,j+nums[i]]
7. return f[len(nums)-1,target]
```
#### optimal structure
f[ i, j ] = f[i-1, j- nums[i] ] + f[i-1, j+nums[i]]
#### correctness 
用f[i, j]表示前i个元素组成j的不同方案数量。
那么前i个元素加上第i+1个元素的可表示的数分别为，
j+nums[i+1]和j-nums[i+1].
例如输入nums= [1,1,1,1,1]，target =3
有如下的状态转移表格：

|     | -5  | -4  | -3  | -2  | -1  | 0   | 1   | 2   | 3   | 4   | 5   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0   |     |     |     |     | 1   |     | 1   |     |     |     |     |
| 1   |     |     |     | 1   |     | 2   |     | 1   |     |     |     |
| 2   |     |     | 1   |     | 3   |     | 3   |     | 1   |     |     |
| 3   |     | 1   |     | 4   |     | 6   |     | 4   |     | 1   |     |
| 4   | 1   |     | 5   |     | 10  |     | 10  |     | 5   |     | 1   |
而我们想要知道的是组合成target=3时的方案数量，查表可得f[4,3] = 5
#### complexity
两层循环，外层循环执行n次，内层循环执行m次，其中m是输入的数组元素和的两倍，总的复杂度为O(mn). 还可以进一步优化，因为每次更新的时候是只会向着下一层的相邻两个块更新的，优化后时间复杂度应该为O(n^2).