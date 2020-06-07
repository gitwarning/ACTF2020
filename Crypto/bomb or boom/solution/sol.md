新人赛的难题作为校赛中等题，5个压缩包破四个，还好吧，所以就弄了更多有趣的编码，第一个是培根不用多说，第二个本来想放摩斯，但觉得太简单就放了盲文，第三个用的是千千秀字的文本转音符（大可搜索一下，如何把文本加密为音符，仅此一家，ps.看着音符的样子难道不好看嘛），第四个是aaencode（学过web应该都知道的吧），第五个是brainfuck，参考一下资料即可。

然后用门限方案的脚本直接跑，就可以辽

```python
import math
from Cryptodome.Util.number import *
import gmpy2
def re(w1,m1):#乘法逆
	t1=w1
	t2=m1
	i=0
	s=[]
	while(t1):
		y=t2%t1
		s.append(int(t2//t1))
		t2=t1
		t1=y
	re1= 0
	re2= 1
	i=len(s)-2	
	while(i>=0):
		t=re2
		re2=re1*1-re2*s[i]
		re1=t
		i-=1
	return re2
def debloom(k):
    x=[]
    m=[]
    for i in range(0,k):
        print("inputs x"+str(i+1)+" and m"+str(i+1)+":")
        x.append(int(input()))
        m.append(int(input()))
    Mn=1
    for i in range(0,k):
        Mn=Mn*m[i]

    w=[]
    for i in range(0,k):
        w.append(int(Mn//m[i]))
    t=[]
    for i in range(0,k):
        t.append(re(w[i],m[i]))
    result=0#初始化
    for i in range(0,k):
        result+=(w[i]*t[i]*x[i])
    result=result%Mn
    print(long_to_bytes(result))

print("input bloom k:")
k=int(input())
debloom(k)

```

![解密图片](.\解密图片.png)