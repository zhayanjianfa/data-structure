#### [Roman to Integer](https://leetcode-cn.com/problems/roman-to-integer/)

```c++
class Solution {

public:
//学习如何答题，能用map吗？能在类里添加属性吗？
//写完代码后，如何自测？
    //leetcode可以输入测试用例测试，但白板的话只能心里面带入算下，我就是带入了最简单的I，发现结束边界未考虑，提前检查出了错误。

//错误记录：
//s.length()写成s.length
//函数没写返回值
//switch每个分支没写break

  int romanToInt(string s) {

 //1 <= s.length <= 15

 //s 仅含字符 ('I', 'V', 'X', 'L', 'C', 'D', 'M')

 //读取一个字符，转换成数字
      //如果后面读不到字符，则将该数字累加，并输出
 	  //如果后面能接着读到字符，则接着读取一个字符，转换成数字
      	//如果比前面的数字小，则将前一个数字累加，接着读
      		//循环
      	//如果比前面的数字大，则将这两个数字合并，即后面的数字减去第一个数字
	int sum = 0;
    int last = 0;
    bool restart = false;
    for(int i=0;i<s.length();i++)
    {
        int temp=0;
        switch(s[i])
        {
            case 'I':
                temp = 1;
                break;
            case 'V':
                temp = 5;
                break;
            case 'X':
                temp = 10;
                break;
            case 'L':
                temp = 50;
                break;
            case 'C':
                temp = 100;
                break;
            case 'D':
                temp = 500;
                break;
            case 'M':
                temp = 1000;
                break;
        }
        if(i==0 || restart)
        {
            if(i+1==s.length())
            {
                sum+=temp;
            }
            else
            {
                last = temp;
            	restart = false;
            }
        }
        else
        {
            //如果上一次的值大于等于本次值，说明后面不可能会有更大的值了
            if(last>=temp)
            {
                sum +=last;
                if(i+1 == s.length())
                {
                    sum+=temp;
                }
                else
                {
                    last = temp;
                }
            }
            //如果上一次值小于本次值，说明这两个字符是一体的
            else
            {
                sum +=temp;
                sum -=last;
                restart = true;
            }
        }
    }

    return sum;

  }

};
```

```
//这里附上官方的代码
class Solution {
private:
    unordered_map<char, int> symbolValues = {
        {'I', 1},
        {'V', 5},
        {'X', 10},
        {'L', 50},
        {'C', 100},
        {'D', 500},
        {'M', 1000},
    };

public:
    int romanToInt(string s) {
        int ans = 0;
        int n = s.length();
        for (int i = 0; i < n; ++i) {
            int value = symbolValues[s[i]];
            if (i < n - 1 && value < symbolValues[s[i + 1]]) {
                ans -= value;
            } else {
                ans += value;
            }
        }
        return ans;
    }
};

```

思路

通常情况下，罗马数字中小的数字在大的数字的右边。若输入的字符串满足该情况，那么可以将每个字符视作一个单独的值，累加每个字符对应的数值即可。

例如 \texttt{XXVII}XXVII 可视作 \texttt{X}+\texttt{X}+\texttt{V}+\texttt{I}+\texttt{I}=10+10+5+1+1=27X+X+V+I+I=10+10+5+1+1=27。

若存在小的数字在大的数字的左边的情况，根据规则需要减去小的数字。对于这种情况，我们也可以将每个字符视作一个单独的值，若一个数字右侧的数字比它大，则将该数字的符号取反。

例如 \texttt{XIV}XIV 可视作 \texttt{X}-\texttt{I}+\texttt{V}=10-1+5=14X−I+V=10−1+5=14。

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/roman-to-integer/solution/luo-ma-shu-zi-zhuan-zheng-shu-by-leetcod-w55p/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

收获：

1.可以在类里添加属性，想必也能添加函数调用。

2.可以使用stl库

3.思路更清晰，代码更简洁

4.map 与 unordered_map区别：https://blog.csdn.net/BillCYJ/article/details/78985895

