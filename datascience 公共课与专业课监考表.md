# datascience 公共课与专业课监考表


---

>>> from datascience import *
>>> public_course=Table().with_columns('Job Number',make_array(100628,100520,100666),'invigilator',make_array('张三','李四','王五'),'public_course',make_array('大学语文','大学英语','高等数学'))
>>> public_course
Job Number | invigilator | public_course
100628     | 张三          | 大学语文
100520     | 李四          | 大学英语
100666     | 王五          | 高等数学
>>> professional_course=Table().with_columns('Job Number',make_array(100666,100321,100123),'invigilator',make_array('王五','李超','张亮'),'professional_course',make_array('计算机网络','操作系统','计算机组成原理'))
>>> professional_course
Job Number | invigilator | professional_course
100666     | 王五          | 计算机网络
100321     | 李超          | 操作系统
100123     | 张亮          | 计算机组成原理
>>> public_course.where('Job Number',are.equal_to(100666))
Job Number | invigilator | public_course
100666     | 王五          | 高等数学
>>> professional_course.where('Job Number',are.equal_to(100666))
Job Number | invigilator | professional_course
100666     | 王五          | 计算机网络




