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



