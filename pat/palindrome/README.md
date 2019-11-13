# 整数与任意进制转化的变形问题
###### 主要是想记录一下我很蠢的一个做法
#### 1.题目描述
如果一个数字从左边读和从右边读一样，那么这个数字就是一个回文数。例如32123就是一个回文数；17在某种意义上也是一个回文数，因为它的二进制型式——10001——是一个回文数。
请你帮忙开发一个程序，判断一个数n在任意进制（2-16）下是否有回文数。
#### 2.输入描述
输入包含多组数据。
每组数据包括一个正整数n (1≤n<2^31)。
#### 3.输出描述
对应每组数据，如果n在2-16进制下存在回文数，则输出“Yes”；否则输出“No”。
## 思路：
- 首先写出自己专属的进制转化函数(●'◡'●)
- 立一个flag！使flag初始值为0
- 要是检测出输入的整数在任一种进制时是回文数，将flag置为1，并跳出循环，输出Yes
- 否则输出No
- 完美通过运行

###### 我可太蠢了，第一遍写的时候，为判断存在回文数，我居然用了一个列表，我可真奢侈！


## Python3代码
    def get(m, n):
        s = ''
        tmp = {0: '0', 1: '1', 2: '2', 3: '3', 4: '4', 5: '5', 6: '6', 7: '7', 8: '8', 9: '9', 10: 'A', 11: 'B', 12: 'C',
            13: 'D', 14: 'E', 15: 'F'}
        while m > 0:
            a = m % n
            m = int(m / n)
            s += tmp[a]
        s = s[::-1]
        return s

    try:
        while True:
            w = int(input())
            flag = 0
            for i in range(2, 17):
                t = get(w, i)
                if str(t)[::-1] == str(t):
                    flag = 1
            if flag == 1:
                print('Yes')
            else:
                print('No')
    except:
        pass