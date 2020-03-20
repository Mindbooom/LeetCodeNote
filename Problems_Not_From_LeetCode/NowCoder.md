牛客网输入输出
1.	使用int main，要求返回或者输出True，False。
使用cout<<”True<<endl,和cout<<”False”<<endl;
2.	输入数组
```c++
    int temp;
    while(cin.peek() != '\n')
    {
        cin>>temp;
        input.push_back(temp);
    }
```
3.	输入字符数组
```c++
    vector<char> str;
    int cou=0;
    while((tem = getchar())!='\n')
    {
        str.push_back(tem);
    }
```
