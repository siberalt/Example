## 1. Примеры обработки запросов
`Примеры кода находятся в файле controllers`

## 2. Примеры SQL-запросов
### Пример 1    

    CREATE FUNCTION `add_node`() RETURNS INT(11) NOT DETERMINISTIC NO SQL SQL SECURITY DEFINER 
    BEGIN 
      INSERT INTO `node`(`status_id`,`creation_date`) VALUES (1,NOW()); 
      RETURN LAST_INSERT_ID(); 
    END


### Пример 2
    SELECT n.`creation_date`,IFNULL(amount_s,0) as amount_s,IFNULL(amount_w,0) as amount_w,IFNULL(amount_f,0) as amount_f,IFNULL(amount_e,0) as amount_e FROM `node` n
    LEFT JOIN (SELECT DATE(n.`creation_date`) as creation_date,COUNT(sn.`id`) as amount_s FROM `node` n, `section` sn WHERE n.id = sn.node_id AND sn.user_id = id 
    GROUP BY n.`creation_date`) s ON s.`creation_date` = n.`creation_date`
    LEFT JOIN (SELECT DATE(n.`creation_date`) as creation_date,COUNT(wn.`id`) as amount_w FROM `node` n, `work` wn WHERE n.id = wn.node_id AND wn.user_id = id 
    GROUP BY n.`creation_date`) w ON w.`creation_date` = n.`creation_date`
    LEFT JOIN (SELECT DATE(n.`creation_date`) as creation_date,COUNT(fn.`id`) as amount_f FROM `node` n, `fact` fn WHERE n.id = fn.node_id AND fn.user_id = id 
    GROUP BY n.`creation_date`) f ON f.`creation_date` = n.`creation_date`
    LEFT JOIN (SELECT DATE(n.`creation_date`) as creation_date,COUNT(en.`id`) as amount_e FROM `node` n, `event` en WHERE n.id = en.node_id AND en.user_id = id
    GROUP BY n.`creation_date`) e ON e.`creation_date` = n.`creation_date`
    GROUP BY `creation_date`

### Пример 3
    CREATE DEFINER=`root`@`localhost` TRIGGER `add_work` BEFORE INSERT ON `work` FOR EACH ROW SET NEW.node_id = add_node()
    
## 3. Примеры верстки
`Примеры кода находятся в файле views`
### Результат верстки 1
![](https://github.com/siberalt/Example/blob/master/bandicam%202020-06-15%2019-39-10-080.jpg)

### Результат верстки 2
![](https://github.com/siberalt/Example/blob/master/bandicam%202020-06-15%2020-15-33-121.jpg)

### Результат верстки 3
![](https://github.com/siberalt/Example/blob/master/bandicam%202020-06-15%2020-56-34-796.jpg)

### Результат верстки 4
![](https://github.com/siberalt/Example/blob/master/bandicam%202020-06-16%2017-51-09-509.jpg)

### Результат верстки 5
![](https://github.com/siberalt/Example/blob/master/bandicam%202020-06-16%2018-26-34-158.jpg)

## Полный код находится в репозиторий https://github.com/siberalt/VKR


  
