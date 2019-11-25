## Tag:
String;medium;
## Description:
Bash语言中常量表示为：
1.[base#]n,base代表基数，即进制。n代表一串待解析数字
2.如果不是第一种形式，则是以0X或者0x开头，代表十六进制。以0开头的常量则是八进制。否则为10进制。
3.基数大于10的数字依次以小写字母a~z,大写字母A~Z,@,_表示。
4.若数字大于基数，非法。

Input:
[2#]111
0X11
120

Output:
7
9
120

## Solution:
```C++
#include <iostream>
#include <vector>
#include<string>
using namespace std;

int main()
{
    string str;
    string result;
    string err = "ERROR";
    string tem;
    int base = 0;
    int pos = 0;
    cin>>str;
    if(str[0]=='[')
    {
        if(str.substr(1,2)=="10") base = 10;
        else {
            base = int(str[1]);
            if (base == 1) base = 10;
            else if (48 <= base <= 57) base -= 48; //0~9
            else if (97 <= base <= 122) base -= 86;//a~z
            else if (65 <= base <= 90) base -= 28;//A~Z
            else if (base == 64) base--;//@
            else if (base == 95) base = 64;//_
            else {
                cout << err << endl;
                return 0;
            }
        }
        int pos = str.find(']');
        result +=str.substr(pos+1,str.size()-3);
    }
    else if(str[0]=='0')
    {
        if(str[1]=='X'||str[1]=='x')
        {
            base = 16;
            result +=str.substr(2,str.size()-2);
        }
        else
        {
            base = 8;
            result +=str.substr(1,str.size()-2);
        }
    }
    else
    {
        base =10;
        result = str;
    }

    int res = 0;
    for(int i=0;i<result.size();i++)
    {
        int temp =int(result[i]);
        if(48<=temp<=57) temp-=48;
        else if(97<=temp<=122) temp-=86;
        else if(65<=temp<=90) temp-=28;
        else if(temp == 64) temp--;
        else if(temp == 95) temp = 64;
        if(temp>=base)
        {
            cout<<err<<endl;
            return 0;
        }
        if(i == result.size()-1)
            res+= temp;
        else
            res=(res+temp)*base;
    }
    cout<<res<<endl;
    return 0;
}

```
## Thought:

题目中坑很多，有许多意外情况的数据难以包含进去，需要细心写代码。不需要一定用ASCII码。
