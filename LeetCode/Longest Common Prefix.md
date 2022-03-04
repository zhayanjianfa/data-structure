1 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] consists of only lower-case English letters.

```c++
class Solution {

//错误记录：substr写成substring
// 遇到结束条件并没有跳出最外面的循环
public:

    //这里我不知道这个公共前缀是否是所有子串共用的意思，如果是这样，题目显得较为简单，先按这个意思来
  string longestCommonPrefix(vector<string>& strs) {
	if (strs.size() == 0)return "";
	if (strs.size() == 1)return strs[0];
	//以最短的子串为标准，遍历所有子串
	char c;
	int length = 0;
	bool end = false;
	for (int i = 0; i < strs[0].length(); i++)
	{
		//获取第一个子串的字符
		c = strs[0][i];
		for (int j = 1; j < strs.size(); j++)
		{
			if (strs[j].length() < i + 1)
			{
				end = true;
				break;
			}
			else
			{
				if (c != strs[j][i])
				{
					end = true;
					break;
				}
				else if (j == strs.size() - 1)
				{
					length++;
				}
			}

		}
			if (end)
				break;
	}
	string result = strs[0].substr(0, length);
	return result;
}

};
```

官方解法里有一种是每两个比较下，然后全部遍历完也可以得到最大的子串

收获：

1.明显看出来官方的算法写法比我要简单很多，哪怕是同一种方法

2.官方的图很有意义，一目了然



得出：算法实现之前的思考很重要，是一种数学上的建模，需要思考透彻。