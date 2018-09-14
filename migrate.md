>要求，创建三张表

lagou_city

lagou_company
 
lagou_position 


#### create table ... as . . 
    select d.id, p.cityName as province, c.cityName as city, d.cityName as district from
    (select * from china_city where depth=3) d
    join china_city c on d.parentId = c.id and c.depth=2
    join china_city p on c.parentId = p.id and p.depth=1;
北京	 北京市	东城区 首先把省市区 分离到lagou_city01表上;

    create table lagou_city as
    select d.id, p.cityName as province, c.cityName as city, d.cityName as district from
      (select * from china_city where depth=3) d
        join china_city c on d.parentId = c.id and c.depth=2
        join china_city p on c.parentId = p.id and p.depth=1
    union
    select c.id, p.cityName as province, c.cityName as city, null as district from (select * from china_city where depth=2) c
      join china_city p on c.parentId = p.id and p.depth = 1;
      
>> 这里注意union的用法：

>Union：对两个结果集进行并集操作，不包括重复行，同时进行默认规则的排序；

>Union All：对两个结果集进行并集操作，包括重复行，不进行排序；

>使用 union 语句虽然会简化语句，但效率会比较低

通过lagou_city表与lagou_position表中的地址相匹配，组合成一张临时表，通过创建一个新的表将需要的字段放进去组合成一张新的表最主要的目的就是要把city列与district列分离出来将lagou_city的city_id列作为外键插入到其中，做到地址表的分离;这样我们就可以做到工作信息，地区信息，分类信息，公司信息分离出来了;

    

>>>总结：首先要把老师提出的问题深度去理解，要对多表查询熟练掌握。
一开始不能急着去敲代码，而是先用思维导图，把自己的思路捋清楚。这样才有一个整体概念，去实现。

      


