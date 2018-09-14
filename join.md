
#### 思路：select * from  s_provinces ajoin s_provinces x on a.id=x.parentId;
#### 先把表搞清楚 和join的用法 然后一步一步去完成↓
#### select p.id,p.cityName,s.cityName,x.cityName from s_provinces p join s_provinces s on s.parentId=p.id join s_provinces x on x.parentId=s.id where p.cityName='广东省'
#### ( 广东省	广州市	荔湾区 )然后用union all将↓链接
#### select s.id,p.cityName,s.cityName,null from s_provinces s join s_provinces p on s.parentId=p.id where p.cityName='广东省';
#### Union：对两个结果集进行并集操作，不包括重复行，同时进行默认规则的排序；
#### Union All：对两个结果集进行并集操作，包括重复行，不进行排序；
