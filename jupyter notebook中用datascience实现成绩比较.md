# jupyter notebook中用datascience实现成绩比较


---
在jupyter notebook中写的代码如下：

from datascience import *
import matplotlib.pyplot as plt
%matplotlib inline

def extract_rank(data,name):
    s=data.where('姓名',are.equal_to(name)).column(11).item(0)
    return s
    
data1=Table.read_table('20211105-utf-8.csv')
data2=Table.read_table('20211106-utf-8.csv')
data3=Table.read_table('20211107-utf-8.csv')
data4=Table.read_table('20211108-utf-8.csv')
data5=Table.read_table('20211109-utf-8.csv')
data6=Table.read_table('20211109-1-utf-8.csv')
data7=Table.read_table('20211110-utf-8.csv')

name1='陈颖'
name2='黄思哲'
name3='周靖珊'

rank1=extract_rank(data1,name1)
rank2=extract_rank(data2,name1)
rank3=extract_rank(data3,name1)
rank4=extract_rank(data4,name1)
rank5=extract_rank(data5,name1)
rank6=extract_rank(data6,name1)
rank7=extract_rank(data7,name1)

rank8=extract_rank(data1,name2)
rank9=extract_rank(data2,name2)
rank10=extract_rank(data3,name2)
rank11=extract_rank(data4,name2)
rank12=extract_rank(data5,name2)
rank13=extract_rank(data6,name2)
rank14=extract_rank(data7,name2)

rank15=extract_rank(data1,name3)
rank16=extract_rank(data2,name3)
rank17=extract_rank(data3,name3)
rank18=extract_rank(data4,name3)
rank19=extract_rank(data5,name3)
rank20=extract_rank(data6,name3)
rank21=extract_rank(data7,name3)

rank_array1=make_array(rank1,rank2,rank3,rank4,rank5,rank6,rank7)
rank_array2=make_array(rank8,rank9,rank10,rank11,rank12,rank13,rank14)
rank_array3=make_array(rank15,rank16,rank17,rank18,rank19,rank20,rank21)

results1=Table().with_columns('考试序号',make_array(1,2,3,4,5,6,7),'姓名',rank_array1)
results1
results2=Table().with_columns('考试序号',make_array(1,2,3,4,5,6,7),'姓名',rank_array2)
results2
results3=Table().with_columns('考试序号',make_array(1,2,3,4,5,6,7),'姓名',rank_array3)
results3

plt.plot(make_array(1,2,3,4,5,6,7),rank_array1,'o--g',label=name1)
plt.plot(make_array(1,2,3,4,5,6,7),rank_array2,'o--r',label=name2)
plt.plot(make_array(1,2,3,4,5,6,7),rank_array3,'o--b',label=name3)

plt.xlabel('历次考试')
plt.ylabel('年级排名')
plt.axis([0,10,650,150])
plt.legend(loc='upper right')
plt.rcParams['font.sans-serif']=['Microsoft YaHei']
plt.grid()
plt.show()

代码运行结果如下图所示：

![此处输入图片的描述][1]


  [1]: https://thumbnail1.baidupcs.com/thumbnail/4e631545fr09ca725acff77eae2e3764?fid=954194626-250528-1014252567781086&rt=pr&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-em356cz4PCaYZ3EuhB35bzJ9obs=&expires=8h&chkbd=0&chkv=0&dp-logid=8824609222802137626&dp-callid=0&time=1669543200&size=c1536_u864&quality=90&vuk=954194626&ft=image&autopolicy=1