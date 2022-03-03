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

